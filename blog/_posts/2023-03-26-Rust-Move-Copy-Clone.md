---
title: Rust Ownership, Move, Copy and Clone
layout: page
---

# Overview

In this post we talk about data/object ownership and how this influences the way Rust works with values such as pass by value, assignment and duplication of objects. We explicitly don't talk about references, that will come in later post.

# Ownership

## Ownership in General

The idea of ownership is a key part of programming in Rust, C, and C++. An "owner" is responsible for releasing associated resources when they are nolonger needed. It's important to realize that a resource may be any number of things such as hardware resources such as memory, or OS resources such as threads, or file system resources, etc., etc.

## Ownership in C

With C, the responsibility of ownership must be conveyed through documentation, naming conventions, etc. and it is up to the programmer to adhere to these conventions. For example, if a function call returns a pointer to a struct, then it must be made clear whether the caller has the responsibility to release it and how. Conversely, if a function call is *provided* with a pointer to a struct, again it must be made clear between the caller and callee if there is a responsibility to release it.

## Ownership in C++

C++ is fully compatible with C and so code can be written in C++ that has all the same requirements as C. However, C++ also has many features oriented towards making ownership explicit. For example, a class constructor initializes an instance of the class, and when that instance goes out of scope or is released, the destructor uninitializes as necessary.

Further discipline on this approach is provided by a C++ idiom called "Resource Acquisition is Initialization" (RAII) which calls for all resource acquisition to be done when intializing an object and all releasing of those resources be done when that object goes out of scope. Smart pointers as `std::unique_ptr<SomeClassName>` are an example of RAII. They own the object they point to and when they go out of scope, will release the object. Another example is guard objects, such as a lock guard, where initializing the guard object acquires the lock and the lock is released when the guard goes out of scope. RAII is particularly important in C++ due to the need to write exception safe code.

It is common to find C++ programs that use a mixture of these old and new styles.

## Ownership in Rust

The offical Rust docs identify the following key tenants of ownership:

> Each value in Rust has a variable that’s called its owner.\\
> There can only be one owner at a time. `*` \\
> When the owner goes out of scope, the value will be dropped (aka destroyed.)

`*`  this is a small lie, for example, Rust supports reference counting which can blur the lines of ownership

Rust has an equivalent to C++'s unique_ptr, which is `Box<>`

## Initialize/Drop

Rust has no formal notion of a constructor like C++ has, in Rust its just a function like any other but a common convention seems to be naming it "new". Implementing the `Drop` trait for a type is roughly equivalent to writing a C++ destructor but there are different rules for when the compiler can do it for you and when not.

```
pub struct NuclearPowerPlant {
    name        : String,
    fuel_amount : u32,
}

impl NuclearPowerPlant {

  pub fn new(name: String, fuel_amount: u32) -> Self {
    acquireUranium(fuel_amount);
    Self { name, fuel_amount }
  }

  pub fn fuel_remaining(&self) -> u32 {
    self.fuel_amount
  }

impl Drop for NuclearPowerPlant {
    fn drop(&mut self) {
        disposeOfUranium(self.fuel_amount);
    }
}
```

Like C++, the compiler will automatically call drop on fields whose types implement Drop.
If all fields of your struct or type have implemented Drop, then the Rust compiler will automatically call them when your variable goes out of scope, otherwise you have to implement Drop by hand.

# Clone/Copy/Move Overview

Going hand in hand with Rust's data ownership rules are the rules for passing data around. Both Rust and modern C++ use many of the same techniques to do this however, Rust has no requirement to be backwards compatible with C and this has led to Rust being able to choose different defaults, be more strict and generally have a different flavour when it comes to passing variables.

*Move* : transfers ownership of data from one variable to another \\
*Copy*: duplicate, using an inexpensive bitwise copy \\
*Clone*: general purpose duplicate, for example that allows for deep copy

Move (the default):
* transfers ownership of data from one variable to another (details for how this happens are in the section below)
* performed implicitly when assignment or pass by value is needed
* after a move, further attempts to access the src will be rejected at compile time
* move is the default behaviour if a type does not implement the Copy trait

Copy:
* allows an instance of a type to be duplicated using an inexpensive bitwise copy
* results in two variables, each of which own's it's data
* performed implicitly when assignment or pass by value is needed
* only types simple enough that they can be duplicated via a simple memcpy can support Copy because Rust does not allow you to reimplement Copy in order to ensure Copy is inexpensive
* opt-in via the Copy trait, which is purely a marker trait that you can think of as a flag turning copy support on/off
* all std primitive types implement Copy, thus copy is relatively common behavior

Clone:
* allows an instance of a type to be duplicated in a general purpose manner
* results in two variables, each of which own's it's data
* can be manually written to perform a _deep copy_
* must be _explicitly_ called because it may or may not be expensive
* any type that cannot be duplicated via a simple memcpy, will automatically support Move and can optionally Clone
* often types that implement Clone and not Copy will have to manually implement Drop as well
* opt-in via the Clone trait

Clone and Copy both create a duplicate but since Clone is more general, if a type supports the simpler Copy, then Rust requires that you say it supports Clone as well.

# Readability

Rust: `foo(my_val);`

Question: Just by looking at this can you tell if my_val is moved to foo or if it is copied?
Answer: no, the only way to know for sure is to check if the type supports the Copy trait.

That said, C++ also has a similar issue:

C++: `foo(my_val);`

Question: Is my_val passed here by value or passed by reference or passed by a const reference?
Answer: In this case, the only way to know is to check the function signature.


### Ownership vs Move and Copy/Clone
Lets clarify what "move" actually does because of it's surprisingly similar to copy:
1. at runtime: a bitwise copy of src to dst is performed, exactly the same as what is performed when the Copy trait is in effect. However, as a result of the bitwise copy, both src and dst might now reference the same resources
2. at compile time: logically, ownership is now said to have been transfered from the src to dst and as a result the compiler treats src as no longer valid
3. since dst now is owner, when it goes out of scope, the Drop trait will be called (aka it's destructor) since src is nolonger the owner, importantly, it's drop is never called.

Note that a copy produces the same result in memory as a move does except the compiler knows the src is still valid and allows continued use of it.

### Why an object might limit clone/copy/move
Every type has one of the following sets of move/clone/copy operations and the following suggests reasons why you might need one over the other:
1. **move only** - Objects for which neither Clone nor Copy support is typically desirable include
singletons, system managers/controllers or those that are tied to a
single physical device or resource, such as a file descriptor.
2. **copy** - usually reserved for trivial types comprised of only primitive data types, for example, a struct that defines an x, y, z position or a vector that defines an angle and a magnitude.
3. **move + clone** - A type that supports Clone but not Copy has additional resources
to account for during the such as threads, strings, files, etc. For example, a String whose characters are stored in a heap buffer and the variable itself is little more than a ptr to the buffer, must be
Clone but not Copy because the simple bitwise Copy would merely copy the ptr but not the
string buffer in the heap.

### Implementing Clone
When all the fields of a struct implement the Clone trait, we can have the
compiler automatically generate the Clone implementation for the struct using the following:
```
#[derive(Clone)]
struct FullName {
    first : String,
    last  : String
}
```

Alternatively, we could manually implement the clone trait as follows:
```
struct FullName {
    first : String,
    last  : String
}

impl Clone for FullName {
    fn clone(&self) -> FullName {
        FullName{first: self.first, last: self.last}
    }
}
```


### Implementing Copy

The Copy trait is not implemented by default and must be opted into. A type such as a struct may implement the Copy trait only if all of it's fields also implement the Copy trait. As a rule of thumb for primitive types, you should support Copy, similar to the convention established by the Rust std library.

Logically a type that supports Copy also supports Clone, so ideally the
compiler would automatically provide a Clone implementation for Copy types (as
Clone can be implemented using the Copy) but current limitations of the type
system prevent it from doing so. Instead, Rust requires that if your type
supports Copy then you must manually supply Clone as well.

A shorthand that tells the compiler to supply the implementation for you is:

```
#[derive(Clone, Copy)]
struct Point {
    x : u32,
    y : u32
}
```

The compiler will reject adding Copy below on the basis that String does not implement Copy:
```
// FAILS due to String not supporting copy
#[derive(Clone, Copy)]
struct FullName {
    first : String,
    last  : String
}
```


### Example: Using Clone + Move

Here we know from the documentation that String supports Clone but not Copy:
```
let name1 = "Kevin".to_string();  // Move used here (from temp result of to_string() to name1)
let name2 = name1.clone();        // Clone used here
let name3 = name1;                // Move used here, name1 is nolonger valid
// println!("{}", name1);  // fails to compile because name1 was moved to name3
println!("{}", name2);
println!("{}", name3);
```

### Example: Using Copy

```
#[derive(Copy, Debug, Clone)] // Copy implies Clone as well
struct Point {
  x : u32,
  y : u32
}

fn add(v1 : Point, v2: Point) -> Point {
  Point{x: v1.x + v2.x, y: v1.y + v2.y}
}

fn test() {
  let x = Point{x: 10, y: 20};
  let y = x;         // Copy trait used here
  let z = x.clone(); // Copy is supported, therefore Clone is too, but it's clunky

  let a = add(x, y); // Copy trait used here
  let b = add(y, z); // Copy trait used here

  println!("a= {:?}, b= {:?}", a, b);
}
```

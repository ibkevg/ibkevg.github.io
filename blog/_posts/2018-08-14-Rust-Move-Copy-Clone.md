---
title: Rust Move, Copy and Clone
layout: page
---

### Overview
Clone means: **An instance of this type can be explicitly duplicated but to do so may require hand written code.**\\
Clone + Copy means: **The compiler is allowed to duplicate an instance of this type automatically using a trivial bitwise copy.**

In C++ terms, a Copy is a shallow copy performed automatically by the compiler whereas Clone allows an
explicit deep copy to be implemented (recognizing that for simple data types there is no distinction between the two.)                   

The absence of the Copy trait means: **when assignment or pass by value are needed, the compiler will move the instance from src to dst instead of copying**

### Ownership vs Move and Copy/Clone
An important aspect of ownership is that the variable that owns the data is responsible for destroying it when it goes out of scope.
When we do a copy from src to dst, we end up with two variables each of which owns it's data and each of which is responsible for dropping (aka destroying) it.
When we do a move from src to dst, the src becomes invalid, dst becomes the owner and is responsible for dropping it.

Now lets clarify what "move" actually does because of it's surprisingly similar to copy:
1. at runtime: a bitwise copy of src to dst is performed, exactly the same as what is performed when the Copy trait is in effect. However, as a result of the bitwise copy, both src and dst might now reference the same resources
2. at compile time: logically, ownership is now said to have been transfered from the src to dst and as a result the compiler treats src as no longer valid, no longer in scope and it's drop is never called
4. at compile time: since dst now is owner, when it goes out of scope, the Drop trait will be called (aka it's destructor) is nolonger the owner, the compiler does not call it's destructor (via the Drop trait).
5. Note that a copy produces the same result in memory as a move does except the compiler knows the src is still valid and allows continued use of it.

### Using clone/copy/move
Every type has one of the following sets of move/clone/copy operations and the following suggests reasons why you might need one over the other:
1. **move only** - Objects for which neither Clone nor Copy support is typically desirable include
singletons, system managers/controllers or those that are tied to a
single physical device or resource, such as a file descriptor.
2. **clone + move** - A type that supports Clone but not Copy typically has additional resources
to account for during the duplication. For example, a String whose
implementation has a heap buffer where characters are stored and a ptr to it, must be
Clone but not Copy because the simple bitwise Copy would merely copy the ptr but not the
string buffer in the heap.
3. **clone + copy** - Note: Copy without Clone is not allowed because Copy represents a characteristic that is additive to Clone.

To use these, clone must be called explicitly, whereas copy and move happen implicitly during assignment or when passing by value.

### Implementing Clone + Move
When all the members of a struct implement the Clone trait, we can have the
compiler automatically generate the Clone implementation for the struct using the following:
~~~
#[derive(Clone)]
struct FullName {
    first : String,
    last  : String
}
~~~

Alternatively, we can manually implement the clone trait as follows:
~~~
struct FullName {
    first : String,
    last  : String
}

impl Clone for FullName {
    fn clone(&self) -> FullName {
        FullName{first: self.first, last: self.last}
    }
}
~~~


### Implementing Clone + Copy

Logically a type that supports Copy also supports Clone, so ideally the
compiler would automatically provide a Clone implementation for Copy types (as
Clone can be implemented using the Copy) but current limitations of type
system prevent it from doing so. Instead, Rust requires that if your type
supports Copy then you must manually supply Clone as well.

A shorthand that tells the compiler to supply the implementation for you is:
~~~
#[derive(Clone, Copy)]
struct Point {
    x : u32,
    y : u32
}
~~~

The compiler will reject adding Copy below on the basis that String does not implement Copy:
~~~
// FAILS due to String not supporting copy
#[derive(Clone, Copy)]
struct FullName {
    first : String,
    last  : String
}
~~~


### Example: Using Clone + Move

Here we know from the documentation that String supports Clone but not Copy:
~~~
let name1 = "Kevin".to_string();  // Move used here
let name2 = name1.clone();        // Clone used here
let name3 = name1;                // Move used here, name1 is nolonger valid
// println!("{}", name1);  // fails because name1 was moved to name3
println!("{}", name2);
println!("{}", name3);
~~~

### Example: Using Clone + Copy

~~~
fn print_u32(val : u32) {
    println!("val={}", val);
}

fn test() {
    let x = 10u32;
    let y = x;         // Copy trait used here
    let z = x.clone(); // Copy is supported, therefore Clone is too, but it's clunky
    print_u32(x);      // Copy trait used here
    print_u32(y);      // Copy trait used here
    print_u32(z);      // Copy trait used here
    println!("x={}, y={}, z={}", x, y, z);
}
~~~

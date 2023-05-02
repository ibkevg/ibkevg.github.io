---
title: Rust Ownership
layout: page
---

In Rust, the concept of ownership is built into the language and enforced by compile-time checks.
Every value has a single owner that determines its lifetime.
When the owner is freed - aka dropped - the owned value is dropped too.

This leads to the formation of ownership hierarchies.

******************************************************************************

This is a good article
https://www.tangramvision.com/blog/c-rust-interior-mutability-moving-and-ownership

******************************************************************************


Chapter 4: Ownership and Moves

Almost all major programming languages fall into one of two camps regarding memory management, depending on which of the two qualities they give up on:
* The “Safety First” camp uses garbage collection to manage memory
* The “Control First” camp leaves you in charge of freeing memory
Rust breaks the deadlock in a surprising way: by restricting how your programs can use pointers. Suffice it to say that some common structures you are accustomed to using may not fit within the rules, and you’ll need to look for alternatives. But the net effect of these restrictions is to bring just enough order to the chaos to allow Rust’s compile-time checks to verify that your program is free of memory safety errors: dangling pointers, double frees, using uninitialized memory, and so on. At run time, your pointers are simple addresses in memory, just as they would be in C and C++. The difference is that your code has been proven to use them safely.

These same rules also form the basis of Rust’s support for safe concurrent programming."



"Rust’s radical wager, the claim on which it stakes its success and that forms the root of the language, is that even with these restrictions in place, you’ll find the language more than flexible enough for almost every task and that the benefits—the elimination of broad classes of memory management and concurrency bugs—will justify the adaptations you’ll need to make to your style."



"Rust’s rules are probably unlike what you’ve seen in other programming languages. Learning how to work with them and turn them to your advantage is, in our opinion, the central challenge of learning Rust."

"In a certain sense, Rust is less powerful that other languages: every other practical programming language lets you build arbitrary graphs of objects that point to each other in whatever way you see fit. But it is exactly because Rust is less powerful that the analyses the language can carry out on your programs can be more powerful. Rust's safety guarantees are possible exactly because the relationships it may encounter in your code are more tractable. This is part of Rust's "radical wager": in practice, Rust claims, there is usually more than enough flexibility in how one goes about solving a problem to ensure that at least a few perfectly fine solutions fall within the restrictions the language imposes.





That said, the concept of ownership as we’ve explained it so far is still much too rigid to be useful. Rust extends this simple idea in several ways:

1. You can move values from one owner to another. This allows you to build, rearrange, and tear down the tree.
2. Very simple types like integers, floating-point numbers, and characters are excused from the ownership rules. These are called Copy types.
3. The standard library provides the reference-counted pointer types Rc and Arc, which allow values to have multiple owners, under some restrictions.
4. You can “borrow a reference” to a value; references are non-owning pointers, with limited lifetimes.

Each of these strategies contributes flexibility to the ownership model, while still upholding Rust’s promises. We’ll explain each one in turn, with references covered in the next chapter."


# My Thoughts

Fair point. But what I think people describe as “the learning curve” is actually the consequence of Rust’s provability rules in combination with the myriad work arounds for the provability rules that had to be built into std. so the learning curve is hitting the complication and then discovering the work around. And yes is it a work around because in C there might be 5 valid solutions to a problem but only 2 of them can be expressed in Rust, so if the programming patterns built into your habits tend to be among the 3 that Rust won't do, then you're going to be frustrated. And you might even be a little offended to learn that to do what you commonly do, you might need to label your code "unsafe". The injustice! ("unsafe" is Rust-speak for unable to be proven safe by the compiler.)

It’s a smaller version of “it’s not practical to use coq to prove a full, real piece of software so you focus on some subset of your real problem and even then have to use tricks to make the proof work.”

Which isn’t to say it can’t find bugs, it’s just that the difference between theory and practice is bigger in practice than it is in theory.



But this is my epiphany: the compiler isn’t saving you from doing stuff, it’s making you do extra stuff

In the case of Rust it’s making you do extra stuff in service of the memory safety bugs.

Forced engineering trade off

Personally I think these things added to a C-like substrate would make a huge difference:
(1) discriminated unions ala Ada
(2) simplified generics (not full Turing complete) to support Rust style return values
(3) traits
(4) typedefs that introduce brand new types instead of aliases
(5) ditch pointers in favour of references

This is close enough to Rust (and Ada actually) that is why I wish Rust ditched the borrow checker rules. If this had been Rust, of course they would never have been funded by Mozilla but I think embedded adoption would be much more rapid.




# Compared to Ada

HadrienG

4
May '19
Having extensively used both Rust and Ada, I find it difficult to see them as overlapping or fighting for the same niche. The two languages/communities put focus on very different things:

Rust gives a lot of flexibility to library writers, Ada is a much more opinionated language that puts a high focus on first-class language support for desired code patterns. Many Ada language features would only exist as libraries in other languages, but are not even implementable as a library in Ada (especially in the concurrency area).
Rust tries hard to be easy to interface to C/++ or bare metal, even if that constrains its type system. Ada has a lot more features that are extremely comfortable to use but don't work well in FFI or without a runtime.
Rust has an unhealthy obsession with pointer types, Ada has an unhealthy obsession with arithmetic types (and to a much lesser extent arrays).
Rust's main open-source compiler receives feature updates every six weeks, Ada's main open-source compiler is updated once a year, mostly for bugfixing (sadly, language complexity makes compilers harder to implement...).
Because of this, Rust makes conservative people anxious, whereas Ada takes a lot of effort to appease them with plenty of certification and paid support contracts.
Everyday Rust features are easy to keep in one's head after a few months of use (though advanced features will obviously take more time), whereas Ada has many corner cases that require keeping the RM close by even after a few years of use.
Rust can be hard to read/understand because it's too terse/magical and the logic is invisible, whereas Ada can be hard to read/understand because it's too verbose and the logic is drowned in noise.
Thankfully, there are also commonalities between the two languages:

Both languages make polymorphism a lot more explicit than is the norm elsewhere.
Both languages encourage error avoidance through very strong typing.
Both languages use strongly typed contracts for generics.
Both language communities strongly dislike undefined behavior.
Both language communities have a serious hubris problem when it comes to comparing themselves with the C/++ world.
If you will tolerate a lame metaphor, Rust feels like a box of woodworking tools while Ada feels like a CNC machine. The latter is a lot more sophisticated than the former, and does a lot more out of the box, but is also more specialized towards a specific kind of work. It's unbelievably effective for its intended purpose, but feels more awkward when used for other purposes.

HadrienG

1
May '19

 L0uisc:
As a complete outsider to Ada, what do you mean with “obsession with arithmetic types”?
Like most other programming languages that I know of, Rust provides a simple abstraction of common machine types (via [i|u][8|16|32|64|size] and f[32|64]) and stops there. Ada takes it much further.

First of all, you are encouraged not to think in terms of what the machine can do, but in terms of what you want to do. This means that you can create integer types defined by their range of accessible values, floating-point types defined by their number of significant digits... and the compiler will pick the most suitable machine type for you given these constraints. In general, the language makes a large effort to significantly decouple the specification of arithmetic types (what you want from them) and their representation (how they're mapped to hardware).

One "problem" is that in many cases, the compiler-selected machine type will do too much and allows incorrect values. Since the Ada designers are very serious about following specifications in a portable manner, there will be attempts to detect and report such events via compile-time and run-time checks, which is one thing to be mindful of when optimizing the performance of Ada code.

But let's talk about a big positive consequence too. Bitfields and exotic integer types (such as those 10-bit ints from DSPs) are much more naturally expressible in Ada than in other languages, because you can much more naturally manipulate, say, 48-bit integers throughout your entire codebase, and not just fail at the point of inserting things in your bitfield where you realize that your 64-bit machine integer does not really fit in 48-bits. This flexibility in representing exotic integer types is, I believe, one reason why Ada remains popular in embedded developments to this day.

A natural consequence of this specification-based reasoning is also that everyone is going to want to define their own integer/float type, so Ada has first-class support for defining multiple incompatible integer and floating-point types, which can only interact with each other through explicit conversion. As you may imagine, this is super-convenient when you want to implement things like units of measurement (the good old Miles vs Meters types), but can also complicate interaction between libraries written by two different groups of people.

Ada also has first-class support for fixed-point arithmetic, which means using integers to represent fractional quantities (e.g. one possible mapping would be that 0.01 is represented as the machine integer 1, -4.2 is represented as the machine integer -420, and so on), and for all intents and purposes these look like floats in Ada code. I can only imagine that this is super-convenient when targeting those hardware architectures that do not have an FPU, although I never programmed those myself.

These are the main ones that I can remember off the top of my head.




//----------------------------------------------------------------------------

// In Rust, const is effectively an alias for a compile time literal value.
// So consts are unlike normal variables in that const values are not stored anywhere at runtime.
// For example, you can create a fixed-sized array, whose size must be specified at compile time,
// using a const, but you can't do that with a let binding.
//
// So you might then think that "mut" is meant to be the rough Rust equivalent to const in C++
// however, C++ constness and Rust mutability are surprisingly different.
//
// OWNERSHIP VS MUT
// Unlike C++, where constness cannot be removed except by casting it away, in Rust, when a
// variable becomes the owner of data, it is free to also determine it's mutability, and that
// includes changing it from what it was before. The previous owner nolonger has a say.
//
// So, if you have a variable that owns data, you can still mutate the data even if the variable
// wasn’t declared as mut. You just have to move it to a mutable variable. This can be done in
// several ways. One is by direct assignment:
//   let mut newvar = oldvar;
// Another is when you call a function and pass an argument by value (ie. the argument is moved
// into a function parameter.) The compiler will let you pass an immutable variable to a function
// that takes a mut variable because the new owner is allowed to determine the mutability.
//
// REFERENCES AND MUTABILITY
// In Rust, mut means first and foremost "exclusive access". &mut T is an exclusive read/write
// access reference whereas &T is a shared, read-only reference. &T and &mut T primarily exist in
// support of providing aliasing information to the compiler, not constness. This is valuable
// because the compiler can do a better job of optimization when it understands whether or not
// pointers are aliased. This also has an advantage for multi-threading which we will discuss later.
//
//
//
// Rust does not let you modify data through a shared reference.
//
// The mut property you might think of as constness, is an attribute of the binding not the data.
//
//

// Most notably, some types feature interior mutability and can be mutated via &T (shared references): Cell, RefCell, Mutex, etc.



// The magic then that allows Sync things to be mutated is ‘interior mutability’
// Interior mutability provides a way to mutate things behind ‘immutable’ (i.e. shared) references.
//
// In a concurrent setting, e.g. Mutex can be used to provide exclusive mutable access to a value.
// So to mutate a shared box you put a Box in a Mutex in an Arc.
//----------------------------------------------------------------------------
fn rebind(mut name : String) {
    name.push_str(" is me");
    println!("rebind says name={}", name);
}

// If you own a variable, you can mutate it, even if it wasn’t declared with mut. But in that
// case, to mutate it, you first have to reassign it with local let mut var = ...
//
// The “mutability” of an owned variable is property of the variable itself, not a data behind
// it. When you say let mut x = y; where y is not mutable, you create a new mutable variable x
// and bind it to the data bound to y. That is you can’t mutate a piece of data behind of
// immutable variable y, but you can do it once it's behind mutable variable x. And, unless
// data in y is Copy, it is moved to x in the example, so you can’t use y after the
// let mut x = y;. That’s the base of Rust’s memory safety guarantee.
// The data can be the same, but the variables (bindings) are different.
//
// Because of internal mutability (Mutex, Cell, RefCell, etc.), it can be very helpful to think
// about mutability as if it were “exclusiveness”.
//
// If you, exclusively, with no mutable or immutable borrows, own something, you can move it
// around and allow it to be mutated as much as you want in the future.
// A mutable borrow is exclusive, and thus allows direct mutation.
// An immutable borrow isn’t exclusive, thus no direct mutation, but you can always then have
// a control structure like a Mutex which schedules at runtime who is exclusively using an
// object, and thus a non-exclusive immutable borrow can mutate data.
//----------------------------------------------------------------------------
pub fn go() {
    println!("---------- rpl_4_ownership ----------");

    let name = "Kevin".to_string(); // not mutable

    // Mutability is a property of the binding and so moving name
    // into name_2 effectively rebinds it, in doing so we're free to
    // make the new binding mutable.
    let mut name_2 = name;

    name_2.push_str(" Goodman");

    println!("name_2={}", name_2);

    // When passing things by value (without & or &mut), mutability is completely a concept
    // on variables, not on types.

    // Let's say you wanted a C++ auto v = std::vector<const crap>, in Rust there is no such thing.
    // In Rust the const would apply only to "v" itself

    // https://users.rust-lang.org/t/why-does-the-compiler-complain-about-vec-mut-tcpstream/3113
    // There is no Vec<mut TcpStream>, because mutability is a concept on the outermost
    // variable, in this case the Vec. If the Vec is mut, anything inside it can also be
    // accessed mutably. If the Vec isn’t mut, everything inside it can only be accessed
    // immutably (without some sort of lock).
    //
    // One other thing: because you are returning a Vec itself, instead of a reference, you
    // don’t decide the mutability. When you pass full ownership of something, the new owner
    // has full control over whether it’s mutable or not, so there’s no need to declare it mut
    // at all. You’ll only need to when you assign the result of the function to a variable.
    //
    // Taking ownership, by using TcpStream instead of something like &TcpStream, means that
    // something is mutable.
    // If you own something, you can do whatever you want to it. There’s no way to express
    // “You take ownership of this thing, but you can’t mutate it” because that’s contrary to
    // the definition of ownership.
    let name_3 = "Goodman".to_string();
    rebind(name_3);
}

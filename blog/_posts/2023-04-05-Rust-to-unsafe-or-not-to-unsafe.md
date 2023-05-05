---
title: Rust To unsafe or not to unsafe?
layout: page
---

# Overview

Safety is a such a driving design goal of the Rust language you might reasonably expect to find that the Rust standard libraries are a shining example of safe code. They are but perhaps not in the way that you might expect because the Rust standard libraries themselves contain `unsafe` code, a Get out of Jail Free card for breaking the language safety rules.

For example, bidirectional linked lists are often cited as an example of a data structure that is tricky to build both efficiently and in accordance with Rust safety rules (due in part to Rust's expectation of hierarchical data ownership, see [*Learn Rust With Entirely Too Many Linked Lists*](https://rust-unofficial.github.io/too-many-lists/)). Sure enough we find:

> rust/library/alloc/src/collections/linked_list.rs: ~1000 lines src, 59 instances of unsafe = ~16 lines per unsafe

So what about the rest of the standard libraries then?

> rust/library/{core,std,alloc}: 128841 lines of src, 4471 instances of unsafe = 28.8 lines per unsafe

So how can a language that claims to be safe, be itself chock full of unsafe code?
Is this a case of "do as I say, not as I do?"

# unsafe wrapping

The usual purpose for a language's standard library is to provide a set of commonly needed helper routines, containers, etc. This is of course true for Rust too but Rust has an additional purpose for it's standard library: `unsafe` wrapping.

In order to prove that Rust code is correct, the Rust compiler imposes a much more strict set of rules than other languages. So much so that the strictness of these rules in practice would prevent most useful programs from being written. Thus Rust has an escape hatch, the `unsafe` keyword, that eases some of the restrictions and denotes code where the programmer is responsible for proving correctness. It's a bit of a grand experiment, where a big part of the language development process has been simply to try to write real software within these constraints to discover cases where relaxing the rules is either necessary or would help make writing practical software, easier. General purpose but safe-to-use abstractions/helpers are then proposed to address this need, and provide a wrapper for the necessary unsafe code. This then goes into the std library for everyone to use and is eventually considered a "stable" part of the Rust language.

Blandy et al, elegantly explain this strategy in their book *Programming Rust* as follows: 

>In a certain sense, Rust is less powerful than other languages: every other practical programming language lets you build arbitrary graphs of objects that point to each other in whatever way you see fit. But it is exactly because Rust is less powerful that the analyses the language can carry out on your programs can be more powerful. Rust's safety guarantees are possible exactly because the relationships it may encounter in your code are more tractable. This is part of Rust's "radical wager": in practice, Rust claims, there is usually more than enough flexibility in how one goes about solving a problem to ensure that at least a few perfectly fine solutions fall within the restrictions the language imposes.

Given this, a reasonable concern when considering whether to use Rust is if the Rust community has written software similar enough to what you intend to write that you will not be getting into uncharted, almost research project level, territory and need to create new kinds of `unsafe` wrappers?

There's no easy answer to this short of simply doing some experiments and trying it out for yourself.

# What does unsafe actually do?

Many people assume that `unsafe` disables ALL compiler checks, however, it only relaxes some of the rules. For example, the compiler will still stop uninitialized variables from being used, the borrow checker will still be in effect, and many other safety checks.

So what does `unsafe` actually let you do then? Only the following:

**Dereference a raw pointer:** Example use cases are C interfacing and building abstractions that the borrow checker doesn't understand. Rather than relaxing the borrow checker rules for references, unsafe Rust instead retains them and instead allows full access to pointers.

**Access or modify a mutable static variable:** Rust provability rules rely on local function knowledge only and since global variable usage cannot be understood without a global system usage analysis, Rust doesn't allow them in safe code.

**Call an unsafe function or method or Access fields of unions:** These two have several use cases but a big one is interfacing to C code.

**Implement an unsafe trait**
Useful with marker traits in particular.

Refer to section [Unsafe Rust](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html) in *The Rust Programming Language* for more rationale.

# Using `unsafe` correctly

So if `unsafe` will be necessary at times, how can you know if what you've written is any good? The Rustonomicon ([https://doc.rust-lang.org/nomicon](https://doc.rust-lang.org/nomicon)), is the official document that describes what considerations are needed when writing `unsafe` code. Aside from being an interesting read with concise descriptions of the rules the compiler expects `unsafe` to abide by, it also offers examples where you might find yourself needing to use unsafe code and suggestions for ways to address it.

# Other Considerations

# Learning Complexity

We can now understand at least some of the complexity of coming to grips with Rust programming as:

  1. the need to adapt your design techniques to those that make the best of Rust's provability rules and the work arounds built into the Standard Library (thus far)
  2. distinguishing between cases that can be solved by judicious application of the standard library from cases that truly need `unsafe` may be difficult. It takes experience to have deep enough knowledge of the std library to be able to recognize when there is something in it that will help you and this is experience that will be hard won since the stdlib will be full of solutions to problems that you will initially not have experienced. This issue is at least mitigated by the helpful community.
  3. tension between "machine provable safety" enforced by the compiler at all times and other design qualities that are not but may at times be more important such as performance or development velocity
## Third Party Crates/Libraries

A great strength of `cargo` and Rust crates is the wide availabilty of 3rd party libraries. However, a potential issue is the uncertain correctness of their usage of `unsafe`. While the Rust standard libraries have language experts reviewing unsafe usage (in addition to the community at large), 3rd party crates may not have such vetting.


## Coding Standards vs Unsafe

Coding standards are a common requirement in safety-oriented development processes. They typically include both requirements and best practices to rein-in easy to misuse parts of the language. For example, a C language standard may say: "goto shall be used only to jump forwards and not, for example, to create loops.". Similarly, in Rust, it's easy to imagine well intended limits being placed on the use of `unsafe`. However, given that `unsafe` is such an important part of the Rust provability strategy, overly draconian limitations could lead to serious problems.


# Appendix

These tests were run April 5, 2023. They are meant to give a rough idea of lines of code, excluding unit tests, benchmarks, whitespace and comments.

**rust/library**
```
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | wc -l
  344633
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | grep unsafe | wc -l
   23922
```

**rust/library/core**
```
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | wc -l
   50568
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | grep unsafe | wc -l
    1546
```

**rust/library/std**
```
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | wc -l
   60021
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | grep unsafe | wc -l
    1968
```

**rust/library/alloc**
```
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | wc -l
   18252
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | grep unsafe | wc -l
     957
```
**rust/library/stdarch/crates/core_arch/src**
```
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | wc -l
  195918
$ find . -name "*.rs" | grep -v test | grep -v bench | xargs -n 1 grep -v // | grep "\S" | grep unsafe | wc -l
   18989
```
10.3 lines per unsafe

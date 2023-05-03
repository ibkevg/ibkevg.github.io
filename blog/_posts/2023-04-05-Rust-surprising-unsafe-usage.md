---
title: Rust Surprising Amount of Unsafe Usage
layout: page
---

# Overview

Given the much vaunted safety of the Rust language you might reasonably expect that the Rust standard libraries are a shining example of safe code. The usual purpose for a language's standard library is to provide a set of commonly needed helper routines, containers, etc. This is of course true for Rust too but Rust has an additional purpose for it's standard library: `unsafe` wrapping.

# unsafe wrapping

In order to prove that Rust code is correct, the Rust compiler imposes a much more strict set of rules than other languages. So much so that the strictness of these rules in practice would prevent most useful programs from being written. Thus Rust has an escape hatch that eases some of the restrictions, the `unsafe` keyword, that denotes code where the programmer is responsible for proving correctness. It's a bit of a grand experiment, where a big part of the language development process has been simply to try to write real software within these constraints to discover cases where relaxing the rules is either necessary or would really help write practical software. Safe abstraction/helper routines are then proposed/designed/built to wrap the necessary unsafe code. This then goes into the std library for everyone to use and is eventually considered a "stable" part of the Rust language.

Blandy et al, elegantly explain this in their book *Programming Rust* as follows: 

>In a certain sense, Rust is less powerful than other languages: every other practical programming language lets you build arbitrary graphs of objects that point to each other in whatever way you see fit. But it is exactly because Rust is less powerful that the analyses the language can carry out on your programs can be more powerful. Rust's safety guarantees are possible exactly because the relationships it may encounter in your code are more tractable. This is part of Rust's "radical wager": in practice, Rust claims, there is usually more than enough flexibility in how one goes about solving a problem to ensure that at least a few perfectly fine solutions fall within the restrictions the language imposes.

Given this, a reasonable concern when considering whether to use Rust is if the Rust community has written software similar enough to what you intend to write that you will not be getting into uncharted, almost research project level, territory and need to create new types of unsafe wrappers? There's no easy answer to this short of simply doing some experiments and trying it out for yourself.

Also since the very nature of the language development process is highly incremental - not in itself a criticism - are the features that currently exist fully baked enough for use in a complex system? `async` is an example of a feature that has received much ongoing attention in recent years. Someone who adopted this feature 2 years ago, would have a quite a different experience than today and again in a couple more years. (This is also where careful consideration is necessary between using official epoch releases and the more commonly used 6 week "stable" releases.)

# unsafe in the standard library

So hopefully we've shown that it's not surprising to find `unsafe` in the standard libraries but it may surprise you to see just how much:

> rust/library/{core,std,alloc} \\
> 128841 lines src \\
> 4471 instances of unsafe \\
> 28.8 lines per unsafe

Bidirectional linked lists are often cited as an example of a data structure that is tricky to build efficiently in Rust, due to Rust's expectation of hierarchical data ownership (see https://rust-unofficial.github.io/too-many-lists/). Sure enough we find:

> In alloc/.../linked list its about: \\
> 1000 lines src \\
> 59 instances of unsafe \\
> 16 lines per unsafe

This explains at least some of the complexity of coming to grips with Rust programming:
  1. you have to adapt your design techniques to make the best of what Rust can prove is correct
  2. a consequence of Rust’s provability rules in combination with the myriad work arounds in stdlib for those provability rules is when you do get stuck, you have to have deep enough knowledge of the std library to be able to recognize when there is something in the std library that will help you (which is initially tricky since it will be full of solutions to problems that you haven’t yet experienced)
  3. otherwise, you might eventually come to decide that the problem you are having is not due to inexperience but rather you will have to come up with your own unsafe abstraction.

# `unsafe` and The Rustonomicon

The Rustonomicon is the official document that describes what considerations are needed when writing `unsafe` code. Aside from being an interesting read with concise descriptions of the rules the compiler expects `unsafe` to abide by, it also offers examples where you might find yourself needing to use unsafe code and suggestions for ways to address it.

https://doc.rust-lang.org/nomicon

# Coding Standards vs Unsafe

Coding standards are a common requirement in safety oriented development processes. They typically include both requirements and best practices and typically rein-in easy to misuse parts of the language, such as "goto shall be used only to jump forwards", for example. Similarly, in Rust, it's easy to imagine well intended limits being placed on the use of `unsafe`. Given that `unsafe` is such an important part of the Rust provability strategy, overly draconian limitations could cause serious problems. It would be easy imagine even small limits being placed on `unsafe` usage that engineers simply avoid it altogether to avoid the hassle, to the detriment of one or more measures of software quality, such as performance or maintainability.

# Data

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

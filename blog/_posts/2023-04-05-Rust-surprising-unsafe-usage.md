---
title: Rust Surprising Amount of Unsafe Usage
layout: page
---

# unsafe usage in the Rust std libraries

The usual purpose for a language's standard library is to provide a set of commonly needed helper routines, containers, etc. This is of course true for Rust too but Rust has an additional purpose for it's standard library: `unsafe` wrapping.

In order to be able to prove that Rust code is correct, the Rust compiler imposes a much more strict set of rules than other languages. The strictness of therse rules means that very few useful programs could be created using the Rust compiler without an escape hatch that lets you disable some of the restrictions. Rust provides this via the `unsafe` keyword which denotes code where the programmer is responsible for proving correctness. A big part of the language development process has been to discover the need for and then create safe abstractions and helpers that wrap unsafe code. This then goes into the std library for everyone to use.

So it's not surprising then to find `unsafe` in the standard libraries but it may surprise you to see just how much:

> rust/library/{core,std,alloc}
> 128841 lines src
> 4471 instances of unsafe
> 28.8 lines per unsafe

Bidirectional linked lists are often cited as an example of a data structure that is tricky to build efficiently in Rust, due to Rust's expectation of hierarchical data ownership (see https://rust-unofficial.github.io/too-many-lists/). Sure enough we find:

> In alloc/.../linked list its about:
> 1000 lines src
> 59 instances of unsafe
> 16 lines per unsafe

This explains at least some of the complexity of coming to grips with Rust programming:
  1. you have to adapt your design techniques to make the best of what Rust can prove is correct
  2. a consequence of Rust’s provability rules in combination with the myriad work arounds in stdlib for those provability rules is when you do get stuck, you have to have deep enough knowledge of the std library to be able to recognize when there is something in the std library that will help you (which is initially tricky since it will be full of solutions to problems that you haven’t yet experienced)
  3. otherwise, you might have to come up with your own unsafe thing. However, many teams probably have coding standard rules against using unsafe, plus many people will be perfectionist enough to spend a *lot* of time trying not to use unsafe when it may in fact be the best thing to do

Blandy et al, explain this in their excellent book *Programming Rust* as follows: 

>In a certain sense, Rust is less powerful that other languages: every other practical programming language lets you build arbitrary graphs of objects that point to each other in whatever way you see fit. But it is exactly because Rust is less powerful that the analyses the language can carry out on your programs can be more powerful. Rust's safety guarantees are possible exactly because the relationships it may encounter in your code are more tractable. This is part of Rust's "radical wager": in practice, Rust claims, there is usually more than enough flexibility in how one goes about solving a problem to ensure that at least a few perfectly fine solutions fall within the restrictions the language imposes.

# Data

Captured April 5, 2023

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

---
title: Rust Strictness vs Prototyping
layout: page
---


# Tension between "Machine Provable Safety" and other Characteristics

There are many quality measures that apply to software in varying degrees depending on the system. For example: performance, correctness and safety, maintainability, portability, testability, etc. In addition, projects have different needs at different phases of development. Early in a project it will often be necessary to rapidly prototype ideas to derisk ideas you're not sure will be able to meet requirements, whereas late in development, 

Having provable safety built into the language is simultaneously a boon and a bane. Certainly, there will be some projects or parts of projects for which machine provable safety is the quality measure that should dominate all other concerns. However, other projects may have other needs as well.

Putting aside the unsafe keyword for now, by using Rust you will ensure code that is not provably safe cannot be written. This is the only quality property that the compiler will guarantee. Other properties may also be important but the compiler will have no opinions.




Also since the very nature of the language development process is highly incremental - not in itself a criticism - are the features that currently exist fully baked enough for use in a complex system? `async` is an example of a feature that has received much ongoing attention in recent years. Someone who adopted this feature 2 years ago, would have a quite a different experience than today and again in a couple more years. (This is also where careful consideration is necessary between using official epoch releases and the more commonly used 6 week "stable" releases.)

# Appendix: `unsafe` in the standard library

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

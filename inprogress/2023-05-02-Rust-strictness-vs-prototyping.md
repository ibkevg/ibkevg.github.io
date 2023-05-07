---
title: Rust Strictness vs Prototyping
layout: page
---


# Tension between "Machine Provable Safety" and other Characteristics

There are many quality measures that apply to software in varying degrees depending on the system. For example: performance, correctness and safety, maintainability, portability, testability, etc. In addition, projects have different needs at different phases of development. Early in a project it will often be necessary to rapidly prototype ideas to derisk ideas you're not sure will be able to meet requirements, whereas late in development, 

Having provable safety built into the language is simultaneously a boon and a bane. Certainly, there will be some projects or parts of projects for which machine provable safety is the quality measure that should dominate all other concerns. However, other projects may have other needs as well.

Putting aside the unsafe keyword for now, by using Rust you will ensure code that is not provably safe cannot be written. This is the only quality property that the compiler will guarantee. Other properties may also be important but the compiler will have no opinions.




https://medium.com/@victor.ronin/love-hate-relationship-with-rust-language-part-2-c36f57d5485d



Pepitoscrespo
3 days ago

In Perl for instance, there indeed exists a no strict directive to disable strictness checks temporarily for cases like prototyping. However, Rust does not have an equivalent feature. Despite that, you can still simplify prototyping in Rust by following these points(annoying i know but it is rusty philosophy) :

1.- Use Option or Result types for basic error handling during prototyping, instead of implementing complex error handling mechanisms.

2.- Utilize interior mutability with Cell, RefCell, or other similar types to avoid some borrow checker issues while prototyping.

3.- Prefer owned types over references to prevent dealing with lifetimes during the prototyping phase.

4.- Apply smart pointers like Box, Rc, or Arc(mentioned already by you) to simplify the ownership model in your prototype, helping you avoid some of the complexity of lifetimes and borrowing.

5.- Avoid concurrency during the initial prototyping phase to keep the code simpler, and introduce it later in the development process once the core functionality has been established.


Also since the very nature of the language development process is highly incremental - not in itself a criticism - are the features that currently exist fully baked enough for use in a complex system? `async` is an example of a feature that has received much ongoing attention in recent years. Someone who adopted this feature 2 years ago, would have a quite a different experience than today and again in a couple more years. (This is also where careful consideration is necessary between using official epoch releases and the more commonly used 6 week "stable" releases.)

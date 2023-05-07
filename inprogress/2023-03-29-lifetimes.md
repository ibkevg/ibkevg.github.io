---
title: Rust Lifetimes and References
layout: page
---


> The first rule of Rust references is that you don't talk about Rust references

# References must always be valid

The first rule of references is that they must always be valid - that is to say you can't create a reference to a variable that will go out of scope or be destroyed before the reference does. Imagine a function that returns the address of a local variable or a use-after-free bug.

Seems simple enough however, this introduces complications related to lifetimes of data that we'll talk about in another post. For example, if you want a struct to contain a reference, then you will have to describe the lifetimes involved so that the compiler can ensure that an instance of your struct - which contains a reference - does not outlast the value that is being referenced. This introduces a whole layer of lifetime syntax, not present in a language like C or C++, whose purpose is to describe the needed lifetimes.

# Lifetimes


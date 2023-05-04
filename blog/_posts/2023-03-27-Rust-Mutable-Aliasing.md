---
title: Performance, Rust References and Mutable Aliasing
layout: page
---

# Performance, Rust References and Mutable Aliasing

> The first rule of Rust references is that you don't talk about Rust references

## Rust References must always be valid

The first rule of references is that they must always be valid - that is to say you can't create a reference to a variable that will go out of scope or be destroyed before the reference does. Imagine a function that returns the address of a local variable or a use-after-free bug.

This hardly seems interesting or even new: languages have had references for decades. Ada introduced this to military software in the early 80s and C++ got references in the 90s. But notice how I said "can't" instead of "shouldn't". In Rust the compiler ensures it's not even possible. Keep in mind it's not like you are a passive participant here and the compiler does all the work. In C++ this is the programmer's responsibility to ensure and in Rust it is also your responsibility except with the additional burden that you have to prove to the compiler that you met your responsibility. For example, if you want a struct to contain a reference, then you will have to prove to the compiler that an instance of your struct does not outlast the value that is being referenced. Sometimes the compiler can infer this but other times it cannot and this introduces a whole layer of clunky syntax for describing these lifetimes, not present in a language like C or C++.

Here is an example of a struct that contains a reference. Because it contains a reference, the compiler needs to ensure that an instance of the struct will outlive the thing the pointer points to. Here `'a` is a lifetime annotation in a struct that contains a reference to a bunch of characters:

```
struct Foo<'a> {
    bar: &'a str,
}
```
It seems like a common cheat people do in Rust if they can't figure out how to make the lifetimes work (ie. get it to compile) is to just use a reference counted pointer.

## Rust References are like Readers/Writer locks

The second rule of Rust references is at any given time you can have either one mutable reference or any number of immutable references.

Anyone who's written concurrent code where data is shared between two threads will be familiar with need to control access to that data due to race conditions. Entire books have been written about techniques meant to address this problem such as mutexes, readers/writer locks, message passing, etc. but, perhaps surprisingly, Rust applies this to even single threaded code. All writable sharing of data via references is statically checked by the compiler almost as though a concurrency protecting readers/writer’s lock was in use.

So why is that?

Aliasing. The idea that more than one pointer could point to the same memory.

## Mutable Aliasing vs Bugs's 

Here are some examples of bugs we can avoid by preventing mutable aliasing:

* *iterator invalidation* - you're iterating through a data structure and delete an element as you go, accidentally invalidating the iterator you're using. Most people using C++ iterators have likely hit this type of issue at least once.

* *Callbacks* - imagine an API that has a callback interface. If the callback function can turn around and call back into the API including even the API function that did the callback in the first place. The API may call this undefined behaviour or it may allow it. If the API hasn't anticipated all the ways a callback could re-enter the API or the user didn't read the documentation then you could have a bug that might have been avoided if mutable aliasing were not possible.


## Mutable Aliasing vs Performance

For years, Fortran could generate faster code than C for vector math due to it's different aliasing rules. Fortran doesn't have pointers, it has formal array types that don't overlap and thus Fortran could assume that function arguments never alias. Over time, various enhancements to C were made, such as C adding the `restrict` keyword to declare that a pointer doesn't alias anything.

Here's some thoughts on this from the C world:
[https://developers.redhat.com/blog/2020/06/02/the-joys-and-perils-of-c-and-c-aliasing-part-1](https://developers.redhat.com/blog/2020/06/02/the-joys-and-perils-of-c-and-c-aliasing-part-1)
[https://developers.redhat.com/blog/2020/06/03/the-joys-and-perils-of-aliasing-in-c-and-c-part-2](https://developers.redhat.com/blog/2020/06/03/the-joys-and-perils-of-aliasing-in-c-and-c-part-2)

Here's some thoughts on this from the Rust world:
[https://doc.rust-lang.org/nomicon/aliasing.html](https://doc.rust-lang.org/nomicon/aliasing.html)

Given that a Rust has more information than a C compiler does about aliasing, in theory Rust may be able to optimize code generated for data access through references/pointers. (It actually took a couple of years to be able to enable these compiler optimizations because compiler backends hadn't been exposed to this much aliasing information before.)

[https://stackoverflow.com/questions/57259126/why-does-the-rust-compiler-not-optimize-code-assuming-that-two-mutable-reference](https://stackoverflow.com/questions/57259126/why-does-the-rust-compiler-not-optimize-code-assuming-that-two-mutable-reference)

Now that it has been enabled for a while, I haven't seen people trumpeting that Rust is faster than C in general and frankly, I tend to distrust benchmarks that as often used for marketing as they are for technical comparison. That said, if you search around you can find benchmarks of various kinds and sometimes Rust is slower, sometimes Rust is faster. So it does seem reasonable to say the two are vary comparable in performance though it's hard to say to what degree the aliasing rules help with this.


## Mutable Aliasing in General

Here's some additional thoughts from the designers of Rust about this topic:

**Niko Matsakis**

"I’ve often thought that while data-races in a technical sense can only occur in a parallel system, problems that feel a lot like data races crop up all the time in sequential systems."
[http://smallcultfollowing.com/babysteps/blog/2013/06/11/on-the-connection-between-memory-management-and-data-race-freedom/](http://smallcultfollowing.com/babysteps/blog/2013/06/11/on-the-connection-between-memory-management-and-data-race-freedom/)

**Manish Goregaokar**

"What I’m going to discuss here is the choice made in Rust to disallow having multiple mutable aliases to the same data (or a mutable alias when there are active immutable aliases), even from the same thread."

[https://manishearth.github.io/blog/2015/05/17/the-problem-with-shared-mutability/](https://manishearth.github.io/blog/2015/05/17/the-problem-with-shared-mutability/)

Reddit comments on Manish's article:
[https://www.reddit.com/r/rust/comments/369jnx/the_problem_with_singlethreaded_shared_mutability/](https://www.reddit.com/r/rust/comments/369jnx/the_problem_with_singlethreaded_shared_mutability/)


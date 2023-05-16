---
title: Performance, Rust References and Mutable Aliasing
layout: page
---

# Performance, Rust References and Mutable Aliasing

A big difference between C and Rust, is unconstrained use of pointers in Rust is allowed only in code tagged as `unsafe`. Ordinary Rust code is limited to using references that are highly constrained in comparison to C pointers. Although C++ also has references too, Rust references are much more constrained than those in C++.

## Rust References must always be valid

The first rule of references is not particularly surprising: references must always be valid - that is to say, you can't create a reference to a variable that will go out of scope or be destroyed before the reference does. So this prevents the creation of a function that returns the address of a local variable or a use-after-free bug.

Now, languages have had references for decades so this type of constraint isn't new or even very interesting. Ada introduced references to military software in the early 80s and C++ got references in the 90s. But notice how I said "can't" instead of "shouldn't"? Rust adds an additional layer where the programmer must also prove to the compiler that they have met their obligation to use references correctly. For example, if you want a struct to contain a reference, then you will have to prove to the compiler that an instance of your struct does not outlast the value that is being referenced. Sometimes the compiler can infer this from the surrounding context but other times it cannot and this leads to new syntax, not present in a language like C or C++, for describing these lifetimes.

Below is an example where `'a` is a lifetime annotation on a struct that contains a reference to some characters. Because the struct contains a reference, the annotation informs the compiler that an instance of the struct must live at least as long as the thing the reference points to.

```
struct Foo<'a> {
    bar: &'a str,
}
```
Lifetimes can introduce a source of complexity that is not always easy to find a solution for (ie. get the code to compile.) Reference counted pointers can become a workaround (crutch?) in these instances, however they come with a performance cost.

## Rust References are like Readers/Writer locks

The second rule of Rust references is at any given time you can have either one mutable reference or any number of immutable references.

Anyone who's written concurrent code where data is shared between two threads will be familiar with need to control access to that data due to race conditions. Entire books have been written about techniques meant to address this problem such as mutexes, readers/writer locks, message passing, etc. but, perhaps surprisingly, Rust applies this to even single threaded code. All writable sharing of data via references is statically checked by the compiler almost as though a concurrency protecting readers/writer’s lock was in use.

Why burden single threaded code with the same constraints as multi-threaded?

The short answer is: *Aliasing*, which occurs when multiple pointers point to the same memory. (See the section below for how the Rust designers themselves justify this decision.)

## Mutable Aliasing vs Bugs's 

Here are some examples of bugs we can avoid by preventing mutable aliasing:

* *iterator invalidation* - you're iterating through a data structure and delete an element as you go, accidentally invalidating the iterator you're using. Most people using C++ iterators have likely hit this type of issue at least once.

* *Callbacks* - imagine an API that has a callback interface. If the callback function can turn around and call back into the API including even the API function that did the callback in the first place. The API may call this undefined behaviour or it may allow it. If the API hasn't anticipated all the ways a callback could re-enter the API or the user didn't read the documentation then you could have a bug that might have been avoided if mutable aliasing were not possible.


## Could Rust Aliasing Rules make it Faster than C?

For years, Fortran could generate faster code than C for vector math due to it's different aliasing rules. Fortran doesn't have pointers, it has formal array types that don't overlap and thus Fortran could assume that function arguments never alias. Over time, various enhancements to C were made, such as C adding the `restrict` keyword to declare that a pointer doesn't alias anything and thus it became possible for C to compete on performance with Fortran in these case. At least for those who understood how to use `restrict` and when to use it.

Here's some further thoughts on this from the C world:
  * [*The joys and perils of C and C++ aliasing, Part 1*](https://developers.redhat.com/blog/2020/06/02/the-joys-and-perils-of-c-and-c-aliasing-part-1)
  * [*The joys and perils of C and C++ aliasing, Part 2*](https://developers.redhat.com/blog/2020/06/03/the-joys-and-perils-of-aliasing-in-c-and-c-part-2)

Here's some thoughts on this from the Rust world:
[https://doc.rust-lang.org/nomicon/aliasing.html](https://doc.rust-lang.org/nomicon/aliasing.html)

Given that a Rust has more information than a C compiler does about aliasing, in theory Rust may be able to optimize code generated for data access through references/pointers. (It actually took a couple of years to be able to enable these compiler optimizations because compiler backends hadn't been exposed to this much aliasing information before.)

[https://stackoverflow.com/questions/57259126/why-does-the-rust-compiler-not-optimize-code-assuming-that-two-mutable-reference](https://stackoverflow.com/questions/57259126/why-does-the-rust-compiler-not-optimize-code-assuming-that-two-mutable-reference)

Now that it has been enabled for a while, I haven't seen people trumpeting that Rust is faster than C in general and frankly, I tend to distrust benchmarks that as often used for marketing as they are for technical comparison. That said, if you search around you can find benchmarks of various kinds and sometimes Rust is slower, sometimes Rust is faster. So it does seem reasonable to say the two are very comparable in performance though it's hard to say to what degree the aliasing rules help with this.


## Thoughts from Rust's Designers

Here's some additional thoughts from the designers of Rust about this topic:

**Niko Matsakis**

"I’ve often thought that while data-races in a technical sense can only occur in a parallel system, problems that feel a lot like data races crop up all the time in sequential systems."

From blog post: [*On the connection between memory management and data-race freedom*](http://smallcultfollowing.com/babysteps/blog/2013/06/11/on-the-connection-between-memory-management-and-data-race-freedom/), in [http://smallcultfollowing.com/babysteps](http://smallcultfollowing.com/babysteps)


Associated reddit thread: [reddit](https://www.reddit.com/r/programming/comments/1g62ga/on_the_connection_between_memory_management_and/)

**Manish Goregaokar**

"What I’m going to discuss here is the choice made in Rust to disallow having multiple mutable aliases to the same data (or a mutable alias when there are active immutable aliases), even from the same thread."

From blog post: [*The Problem With Single-threaded Shared Mutability*](https://manishearth.github.io/blog/2015/05/17/the-problem-with-shared-mutability/), in [https://manishearth.github.io](https://manishearth.github.io)

Associated reddit thread: [reddit](https://www.reddit.com/r/rust/comments/369jnx/the_problem_with_singlethreaded_shared_mutability/)


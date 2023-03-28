---
title: Rust Mutable Aliasing
layout: page
---

# Mutable Aliasing

Anyone who's written concurrent code where data is shared between two threads will be familiar with need to control access to data that is shared. Entire books have been written about techniques meant to address this problem such as mutexes, reader/writer locks, message passing, etc.

Rust also has a no-shared mutable aliasing rule. BUT it applies it even for single threaded code. Basically all writable sharing of data is handled by the compiler almost as though a concurrency protecting readers/writer’s lock was in use.

So why is that?

# Mutable Aliasing vs Bugs's 

Here are some common example of what preventing mutable aliasing protects us from:

* *iterator invalidation* - You're iterating through a data structure and delete an element as you go, accidentally invalidating the iterator you're using. Fair point, I'm sure most people using C++ iterators have hit this type of issue at least once. It should be found through proper unit testing and avoided by experience.

* *Callbacks* - Another example occurs with an API that has a callback interface. The API may call this undefined behaviour or it may allow it. If the callback function can turn around and call back into the API including even the API function that did the callback in the first place and the API hasn't anticipated all the ways a callback could re-enter the API then you could have a bug due to mutable aliasing.

In my personal experience over the past 30 years, I've only encountered a couple bugs attributable to mutable aliasing. So I can't say I felt much excitment over this language design's ability to reduce bugs that I rarely encounter anyways. Especially if the constraint complicates everything else. Time will tell I guess.

Here's some thoughts from the designers of Rust about this topic:

**Niko Matsakis**

"I’ve often thought that while data-races in a technical sense can only occur in a parallel system, problems that feel a lot like data races crop up all the time in sequential systems."
http://smallcultfollowing.com/babysteps/blog/2013/06/11/on-the-connection-between-memory-management-and-data-race-freedom/

**Manish Goregaokar**

"What I’m going to discuss here is the choice made in Rust to disallow having multiple mutable aliases to the same data (or a mutable alias when there are active immutable aliases), even from the same thread."

https://manishearth.github.io/blog/2015/05/17/the-problem-with-shared-mutability/

Reddit comments on Manish's article:
https://www.reddit.com/r/rust/comments/369jnx/the_problem_with_singlethreaded_shared_mutability/


# Mutable Aliasing vs Performance

For years, Fortran could generate faster code than C for vector math due to it's different aliasing rules. Fortran doesn't have pointers, it has formal array types that don't overlap and thus Fortran could assume that function arguments never alias. Over time, various enhancements to C were made, such as C adding the `restrict` keyword to declare that a pointer doesn't alias anything.

Here's some thoughts on this from the C world:
https://developers.redhat.com/blog/2020/06/02/the-joys-and-perils-of-c-and-c-aliasing-part-1
https://developers.redhat.com/blog/2020/06/03/the-joys-and-perils-of-aliasing-in-c-and-c-part-2

Here's some thoughts on this from the Rust world:
https://doc.rust-lang.org/nomicon/aliasing.html

Given that a Rust has more information than a C compiler does about aliasing, in theory Rust may be able to optimize code generated for data access through references/pointers. (It actually took a couple of years to be able to enable these compiler optimizations because compiler backends hadn't been exposed to this much aliasing information before.)

https://stackoverflow.com/questions/57259126/why-does-the-rust-compiler-not-optimize-code-assuming-that-two-mutable-reference

Now that it has been enabled for a while, I haven't seen people trumpeting that Rust is faster than C in general and frankly, I tend to distrust benchmarks that as often used for marketing as they are for technical comparison. That said, if you search around you can find benchmarks of various kinds and sometimes Rust is slower, sometimes Rust is faster. So it does seem reasonable to say the two are vary comparable in performance though it's hard to say to what degree the aliasing rules help with this.

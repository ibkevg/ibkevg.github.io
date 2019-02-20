---
title: Rust References and Borrowing
layout: page
---

### Overview

What I’m going to discuss here is the choice made in Rust to disallow having multiple mutable aliases to the same data (or a mutable alias when there are active immutable aliases), even from the same thread.
https://manishearth.github.io/blog/2015/05/17/the-problem-with-shared-mutability/
https://www.reddit.com/r/rust/comments/369jnx/the_problem_with_singlethreaded_shared_mutability/


I’ve often thought that while data-races in a technical sense can only occur in a parallel system, problems that feel a lot like data races crop up all the time in sequential systems.
http://smallcultfollowing.com/babysteps/blog/2013/06/11/on-the-connection-between-memory-management-and-data-race-freedom/

https://www.reddit.com/r/rust/comments/95ky6u/why_arent_multiple_mutable_references_allowed_in/

https://doc.rust-lang.org/nomicon/aliasing.html



### Misc

variable name binds to an instance of a type (aka object)
An object can be bound to a different variable by moving it


don’t think of & as a pointer, but as a temporary, shared read-only (or &mut exclusive read-write) lock on data.
Note that &/&mut can’t exist without the owned counterpart also existing somewhere else.

I've been playing around with static structs and exploring the consequences of the "can't call a function" limitation.

(1) Prevents initialization from Default::default()
(2) Prevents static data from containing most Clone types. ie. anything that would require a function call to initialize such as String (although in that specific case, replacing it with str may in some cases, be a workaround.) Basically, it's struct is limited to pointers, references and trivial Copy types.


Presumably the goal on the no function call constraint is to side step the static initialization problem of C++, Ada, etc.



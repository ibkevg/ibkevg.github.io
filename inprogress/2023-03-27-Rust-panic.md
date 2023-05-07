---
title: Rust doesn't have exceptions ... or does it?
layout: page
---

# Panics

Panics are quite similar to single purpose exceptions.

https://doc.rust-lang.org/book/ch09-01-unrecoverable-errors-with-panic.html


https://github.com/rust-lang/rfcs/blob/master/text/1513-less-unwinding.md
https://github.com/rust-lang/rfcs/pull/1513

https://github.com/rust-lang/rfcs/blob/master/text/1328-global-panic-handler.md

https://github.com/rust-lang/rfcs/blob/master/text/1236-stabilize-catch-panic.md
https://github.com/rust-lang/rfcs/pull/1236


# Mixing Languages

Imagine a C routine performing a Rust callback and the Rust callback routine panics. The C code can't handle the panic unwind.
Imagine a Rust program calling a C++ function, and it throws a C++ exception, Rust can't handle that.

https://doc.rust-lang.org/std/panic/fn.catch_unwind.html

https://www.reddit.com/r/rust/comments/phws7n/unwinding_vs_abortion_upon_panic/

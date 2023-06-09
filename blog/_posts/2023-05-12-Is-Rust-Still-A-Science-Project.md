---
title: Rust's "Radical Wager"
layout: page
---

* This will become a table of contents (this text will be scraped).
{:toc}

# Introduction

I've been enthusiastic about the *idea* of a better C for many years now.

What initially drew me to Rust was not so much memory safety but rather how massively more expressive and type safe it is than C while at the same time being suitable for environments C is necessary for. It has advanced features such as Ada-style variant records (C union + disciminant), generics, modules, traits and a robust, non-exception-based design for error handling. In theory Rust could even be faster than C code due to it's [different pointer aliasing rules](http://stationaryaction.com/blog/2023/03/27/Rust-Mutable-Aliasing.html).

So I spent time coming to grips with the language back in the 2017/2018 time frame but ultimately bounced off. Rust has a reputation for being difficult to learn and certainly part of the difficulty has to do with learning how to apply all these new language features but what I didn't expect was that Rust is actually two things: a traditional language and a memory-safety-correctness prover. This "prover" part of it's personality has it's own learning curve, such as learning how to choose designs that work within the confines of Rust's provability rules. Also I wasn't expecting correct programs to be rejected because it's memory safety analysis is not always sophisticated enough (or could never be sophisticated enough) to realize that a program is ok. People often refer to this as "wrestling with the borrow checker" but IMHO it's more than that. 

Also, I just generally ran into a number of papercuts, speedbumps and roadblocks. I was shocked at the time to learn that something as simple as a linked list is surprisingly difficult in Rust [*Learn Rust With Entirely Too Many Linked Lists*](https://rust-unofficial.github.io/too-many-lists/). I found the lifetime syntax noisy, ran into cases where correct code was not accepted by compiler, etc. Part of my issue too was that the difficulties were mainly about proving memory safety but when I go back through a list of the nastiest bugs I've ever had to wrestle with, it tends to be dominated by threading issues, unexpected event ordering, deadlocks, interrupts, stack overruns, hardware databook misunderstandings, etc. so do I really want to go to a lot of trouble for memory safety? Generally I felt like using Rust was how I imagined it would be like working in a large bureaucracy, like the federal government: lots of rules in place that were put in place for good reasons but taken together, make it hard to get things done.

Now in 2023, with Linux and Windows making moves to put Rust into the kernel, is now the right time to return?

So this time I decided I need to spend more time understanding the underlying philosophy of Rust as a language to better understand the underlying reasons for some of the complexity that goes beyond traditional languages.

# Rust Provability Rules vs `unsafe`

Memory safety is a such a driving design goal of the Rust language that you might reasonably expect to find the Rust standard libraries are a shining example of machine proven, memory safe, code. So, it may surprise you then to learn that not only does Rust have a Get out of Jail Free card for breaking the language safety rules, the `unsafe` keyword but the Rust standard libraries themselves contain significant amounts of `unsafe` code.

For example, bidirectional linked lists are often cited as an example of a data structure that is tricky to build both efficiently and in accordance with Rust safety rules (due in part to Rust's expectation of hierarchical data ownership, see [*Learn Rust With Entirely Too Many Linked Lists*](https://rust-unofficial.github.io/too-many-lists/)). Sure enough we find:

> rust/library/alloc/src/collections/linked_list.rs: ~1000 lines src, 59 instances of unsafe = ~16 lines per unsafe

Stepping back, we find for the rest of the standard libraries:

> rust/library/{core,std,alloc}: 128841 lines of src, 4471 instances of unsafe = 28.8 lines per unsafe

So how can a language that claims to be safe, be itself chock full of unsafe code? And if the standard library itself needs this large amount of `unsafe`, then shouldn't I expect my programs to need it too?

# `unsafe` Wrapping

The usual purpose for a language's standard library is to provide a set of commonly needed helper routines, containers, etc. This is of course true for Rust too but Rust has an additional purpose for it's standard library: `unsafe` wrapping.

In order to prove that Rust code is correct, the Rust compiler imposes a much more strict set of rules than other languages. So much so that the strictness of these rules in practice would prevent most useful programs from being written. Thus Rust has an escape hatch, the `unsafe` keyword, that eases some of the restrictions and denotes code where the programmer is responsible for proving correctness. (See the section below for more thoughts on working with `unsafe` code, including 3rd Party crates and coding standards.)

It's a bit of a grand experiment really because *a big part of the Rust language development process has been to simply try writing real software within these constraints and discover cases where relaxing the rules is either necessary period or would make it easier to write software that achieves properties other than safety, such as performance.* This leads to the creation of new language features and or general purpose but safe-to-use abstractions to provide a wrapper for the necessary unsafe code. This then goes into the compiler or std library for everyone to use and is eventually considered a "stable" part of the Rust language.

Blandy et al, elegantly explain Rust's provability vs functionality strategy in their excellent book *Programming Rust* as follows: 

>In a certain sense, Rust is less powerful than other languages: every other practical programming language lets you build arbitrary graphs of objects that point to each other in whatever way you see fit. But it is exactly because Rust is less powerful that the analyses the language can carry out on your programs can be more powerful. Rust's safety guarantees are possible exactly because the relationships it may encounter in your code are more tractable. This is part of Rust's "radical wager": in practice, Rust claims, there is usually more than enough flexibility in how one goes about solving a problem to ensure that at least a few perfectly fine solutions fall within the restrictions the language imposes.

To me, the need for the standard library to contain safe to use wrappers for `unsafe` code is both a pro and a con. A pro because it’s a big part of what makes Rust even possible, a con because it takes time for the Rust language designers to come up with safe ways of doing common things and they exist as lingering pain points in the meantime. How much time? Did you know that Rust's first official release was in 2015? 8 years ago.

In a way, you could think that the ongoing need for the `unsafe` keyword implies that Rust is not yet finished. Like shouldn't there come a time when the language as a whole is "good enough" and `unsafe` is no longer required as it was at the beginning? Could it be eliminated or at least decomposed into finer grained controls like C++ did with C-style casting? Might `unsafe` be stripped back to the minimum set of controls needed to support interfacing with other languages like C and assembler? Time will tell but I suspect the answer is no and `unsafe` is here to stay. Refer to Appendix A for a description of what `unsafe` actually provides, it's already surprisingly close to the minimum surface area needed to interface with other languages, it just happens to also work quite well for new Rust language features.

## An Example of `unsafe` wrapping

Let's consider an example of the sort of thing someone coming from a language like C might run into that illustrates how the standard library first made the proveability rules tractable and then over time - a very long time - refined it to be fairly elegant to use.

Imagine you're writing a set of Sudoku puzzle solving algorithms and find that a routine that can rotate the puzzle by 90 degrees would be useful. Your first attempt at such a function might look something like this (since Sudoku puzzles are only 9x9 we'll ignore inplace matrix rotation implementations):

```
pub struct SudokuPuzzle {
    pub grid : [[u8 ; 9]; 9],  // 2 dimensional 9x9 array, comprised of unsigned, 8 bit, values
    ... other stuff ...
}


impl SudokuPuzzle {

    pub fn rotate_90(&mut self) {
      let mut x : [[u8 ; 9] ; 9]; // Uninitialized array that we will immediately init

      // Copy the puzzle grid into x, rotating as we go
      for r in 0..9 {
            for c in 0..9 {
               x[r][c] = self.grid[8-c][r];
            }
      }

      self.grid = x;
    }
}
```

Unfortunately, this won't compile because Rust does not allow an uninitialized array to be created. We could  take the path of least resistence here and just tell Rust to initialize the array with zeroes and maybe if we are in a hurry, this is where we'd have stopped:
```
      let mut x : [[u8 ; 9] ; 9] = [[0;9];9];
```

But doing this will cause the array to be initialized twice, so let's at least *try* to be performant.

You might now decide to just wrap this in `unsafe` and move on, however, `unsafe` doesn't relax the variable intitialization rules, so we need to look for another solution. A short time spent googling will reveal that a std library feature called "MaybeUninit" can be applied as follows but you'll have to hold your nose:

```
    pub fn rotate_90(&mut self) {

        let mut x: [[MaybeUninit<u16>;9];9] = unsafe {
              MaybeUninit::uninit().assume_init()
        };

        for r in 0..9 {
              for c in 0..9 {
                 x[r][c] = MaybeUninit::new(self.grid[8-c][r]);
              }
        }

        self.grid = unsafe { mem::transmute::<_, [[u16;9];9]>(x) };
    }
```

Pretty gross. So we google a bit more and discover that a std lib routine, `from_fn`, was stablized in Rust 1.63 Aug/2022 to help with exactly this problem. We still have to initialize the array but we're nolonger limited to compile time constants and can instead have Rust call a function at runtime for each value as it is initialized. Using a closure, aka anonymous function, we can now write:
```
    pub fn rotate_90(&mut self) {
        let init = |r: usize, c: usize| self.grid[8 - c][r];  // init is a closure

        // Create a temporatory array that is rotated 90 degrees
        let x = array::from_fn(|r| array::from_fn(|c| init(r, c)));

        self.grid = x;
    }
```
`from_fn` is an example of an `unsafe` wrapper that we talked about earlier and you can see exactly how it works it's magic here [library/core/src/array/mod.rs](https://github.com/rust-lang/rust/blob/master/library/core/src/array/mod.rs). Also, you might notice that nowhere do we specify the size of the matrix and that's because Rust's type inference feature figures it out automatically.

For a final bit of clean up we can embed the enclosure right where it's needed in the call chain:
```
    pub fn rotate_90(&mut self) {
        self.grid = array::from_fn(|r|
            array::from_fn(|c|
                self.grid[8 - c][r]
            )
        );
    }
```

To get a better feel for what these versions actually do, use this link [godbolt.org](https://godbolt.org/z/7fodaWfEc), to see the `MaybeUninit` and `from_fn` versions side by side and compare the assembler produced. (Notice that the assembler produced by the `MaybeUninit` version is tighter, perhaps this will improve as the compiler matures?)

That was just one very small example of how Rust rules can lead to some sharp edges and result in software that looks very different from what you might have written in C. So what led to this complexity? Consider this, somewhat similar, case:

```
let mut clipped;

if x <= 10 {
   clipped = x;
} else {
   clipped = 10;
}
println!("clipped={}", clipped);
```
Here the variable `clipped` is also uninitialized, but since the compiler can verify that it is initialized before it's read, that's ok. The case we started with above is similar, but since the type is an array, Rust is not sophisticated enough to allow us to create it uninitialized and confirm through code analysis that we fully initialized it before it is later read from. So it provides an alternative means to accomplish what we want to do in a way that it *can* prove is correct.

And that's the fundamental strength/weakness of the Rust language design. You, the programmer, may be able to see that something Rust is concerned about is not a problem but for one reason or another, Rust cannot. So the language endeavors to provide you with an alternative that it *can* prove is correct. This alternative may or may not be elegant or simple because like most things finding the "simple solution", especially amid complex constraints like the Rust language design, is often hard and takes much longer than finding a quick/dirty solution. This is born out in the progression of solutions Rust offered for the array initialization problem above.

This may also inform whether a project may want to lock themselves to a specific compiler verion. Rust has had three major edition releases so far: Rust 2015, Rust 2018, and Rust 2021. A project that has adopted the latest one as it's standard compiler version, Rust 2021, would find that `array::from_fn` is not available to them. This is perhaps an argument for avoiding being too strict about locking to a specific edition, however safety critical projects that require certified compilers do not have this luxury.

## A Better Example: `unsafe` Wrapping to Placate the Borrow Checker

Someday I'll take the time to write this myself but instead, for now, you can take a look at the source code for the Rust standard library's linked list: [linked_list.rs](https://github.com/rust-lang/rust/blob/master/library/alloc/src/collections/linked_list.rs)

# The Borrow Checker and Local Function Analysis

Here is an example where Rust may reject a perfectly safe program because of limitations in it's analysis abilities (taken from [reddit](https://www.reddit.com/r/rust/comments/1440094/problematic_pattern_ive_encountered_a_few_times/)):

```
struct Foo {
    items: Vec<u32>,
}

impl Foo {
    fn run_all(&mut self) {
        for item in &self.items {
            self.run_one(item);
        }
    }
    
    fn run_one(&mut self, item: &u32) {
        // CODE
    }
}
```
The compiler will fail to compile `run_all()` here because Rust references work like reader/writer locks and disallows an immutable borrow (which occurs at `&self.items`) and a mutable borrow (which occurs at `self.run_one(item)`) at the same time. Rust performs only a local function analysis to determine correctness and thus it assumes *any* operation on that mutable reference could happen in `run_one()` - for example, resizing the vec itself which could invalidate the iterator used in the loop. However, the actual use of `&mut self` at `CODE` may actually be perfectly safe and thus we could analyze this code and assess that it's perfectly memory safe.

Solving a compile error such as this depends entirely on what `run_one()` needs to do with it's parameters.

Another restriction that derives from these borrowing rules is that Rust and circular references don't mix. Rust strongly prefers hierarchically structured data, such as trees.

# So is Rust Still a Science Project?

We can now understand at least some of the complexity of using/learning Rust programming as:

  1. the need to adapt your design techniques to those that make the best of Rust's provability rules and the work arounds built into the Standard Library (thus far)
  2. distinguishing between cases that can be solved by judicious application of the standard library from cases that truly need `unsafe` will take experience. This is experience that will be hard won since the stdlib will be full of solutions to problems that you will initially not have experienced. This issue is at least mitigated by the helpful community.
  3. the tension between "machine provable memory safety" enforced by the compiler at all times and other design qualities that are not enforced by the compiler but may at times be more important such as performance or development velocity

Given that the Rust language design process is to *write software until you hit a roadblock, find a way to relax the rules and continue*, a reasonable concern when considering whether to use Rust is if the Rust community has written software similar enough to what you intend to write that you will not be getting into uncharted, science project level, territory and need to create new kinds of `unsafe` wrappers or even language features?

There's no easy answer and probably the best thing to do is simply try it out for yourself, being careful to use experiments suited to your application domain. However, below we discuss other ways to tilt the odds in your favour.

## Play to Rust's Strengths

One thing you *can* do is concentrate on application domains with the most Rust adoption. Here is the glossy brochure version: [https://www.rust-lang.org/what](https://www.rust-lang.org/what)

**Command Line Tools**
Some of the earliest applications written in Rust were command line tools which I think is a reflection of Rust adoption by hobbyists. `ripgrep` is a fairly well known product of this era and it's pretty easy to find others. For example, this list is a start: [Rust Command Line Utilities](https://github.com/sts10/rust-command-line-utilities).

**Web Services and `async`**
Back-end web services as a domain have received a fair amount of attention in Rust. Several web frameworks exist for Rust, including [Actix](https://actix.rs) and [Rocket](https://rocket.rs). The language has evolved to support webservices in part by the introduction of `async` and associated gear. `async` is an increasingly common language feature used, for example, to reduce resource consumption by threads in large web servers. Adding this feature within the constraints of memory safety has been a complex ongoing effort since 2019 and is still under going refinement to reduce pain points and improve integration with the full language (e.g. async functions in traits are expected to be stabilized in 2023.) It seems that good progress is being made, however, also consider this 2022 article, written by an experienced Rust programmer: [Rust Is Hard, Or: The Misery of Mainstream Programming](https://hirrolot.github.io/posts/rust-is-hard-or-the-misery-of-mainstream-programming.html). Also this: [When to use Rust and when to use Go](https://blog.logrocket.com/when-to-use-rust-when-to-use-golang)

**OS and Embedded**
Recently, the door has been opened for Rust to be used to write Linux drivers. Microsoft is doing the same: [*Microsoft is Rewriting Parts of the Windows Kernel in Rust*](https://www.thurrott.com/windows/282471/microsoft-is-rewriting-parts-of-the-windows-kernel-in-rust) This will likely lead the embedded community to drive Rust enhancements and smooth out rough edges at an accelerated pace. The following enthusiastic twitter thread about success writing a graphics driver received a fair amount of attention in the Rust community: [Lina Asahi](https://twitter.com/LinaAsahi/status/1577667445719912450). A more cautious perspective on working with low level code in Rust is this one: [Rust: A Critical Retrospective](https://www.bunniestudios.com/blog/?p=6375).

## Understand Known Pain Points and Limitations

The other thing you can do is have your eyes wide open regarding pain points. A quick web search will reveal an enormous amount of Rust enthusiasm and advocacy, however, it's also useful to contrast this with more sober criticism.

> "There are only two kinds of languages: the ones people complain about and the ones nobody uses." - Bjarne Stroustrup

**General Surveys**
The following is an interesting analysis written in 2018 (Rust has had three major editions so far: Rust 2015, Rust 2018, and Rust 2021) that describes many of the early pain points and refinements that were introduced to address them: [*Things Rust Doesn't Let You Do*](https://medium.com/@GolDDranks/things-rust-doesnt-let-you-do-draft-f596a3c740a5). Much has been addressed since then but interestingly, a number of items that were identified then are still issues today.

More recently, in 2023 we find non-trivial pain points do still exist, consider this article: [*When Rust Hurts*](https://mmapped.blog/posts/15-when-rust-hurts.html).

Also Graydon Hoare has a nice presentation that includes some honest "what is good/bad about Rust": [Rust for "Modern C++" Devs](http://venge.net/graydon/talks/RustForModernCPPDevs.pdf)

**Deadlocks and Memory Leaks**
An interesting limitation relates to the often advertised feature of "fearless concurrency". This refers to the idea that Rust's memory safety and avoidance of data races extends to multi-threading races as well. While true, and very powerful, deadlocked threads do not violate memory safety provability rules, thus fearless concurrency does not extend to [deadlocks](https://doc.rust-lang.org/book/ch16-03-shared-state.html#similarities-between-refcelltrct-and-mutextarct).

Another interesting limitation is memory leaks. Similar to deadlocks, Rust provability rules do not consider a memory leak to be a memory safety issue. And while Rust provides a number of useful tools to aid in memory/resource management such as reference counting, leaks are still possible, for example, via [reference count cycles](https://doc.rust-lang.org/book/ch15-06-reference-cycles.html).

**GUIs**
Similarly, the state of the Rust GUI ecosystem appears to be still evolving since traditional UI design patterns born out of the OOP/inheritance world require replacement with patterns better suited to Rust's strengths. Several discussions about this can be found online but here are a couple to give you the flavour: [Why is Building a UI in Rust so hard?](https://www.reddit.com/r/programming/comments/114cknb/why_is_building_a_ui_in_rust_so_hard/) and [Advice for the next dozen Rust GUIs](https://raphlinus.github.io/rust/gui/2022/07/15/next-dozen-guis.html).

# Final Thoughts

As adoption by the communities in various development domains grows, so too does Rust's suitability for and usability in those domains.

If memory safety bugs form the bulk of the bugs historically in your bug tracking system or tend to be the ones that have had the most serious repercussions, as was the case for the Mozilla Firefox web browser and lead to the creation of Rust in the first place, then Rust will help you by putting it’s thumb on the scale as you code, forcing you to address these concerns as you go. The cost to you will be proveability constraints that you will be have to get used to/live with and some of these constraints will be the somewhat artificial/arbitrary consequences of the language design community not yet having time to figure out how to elegantly work within these constraints.

If memory safety bugs are *not* a dominant source of defects in your system, the decision becomes more complex. Adoption of Rust for business or mission critical projects should be done cautiously. Perhaps, preceded by pilot projects to evaluate whether it's pain points are serious issues in your environment or not. The memory safety Rust ensures is not free. A Rust programmer still has to write code in a memory safe way and that way has to be one that the compiler can prove. So a team could switch to Rust, and find the small number of memory safety bugs they were experiencing is even smaller now but the high runner type of bugs - deadlocks for example - are not improved plus it takes longer now to write code to satisfy Rust’s proveability rules.


# Appendix A: Working with `unsafe` Code

## What does unsafe actually mean?

Many people assume that `unsafe` disables ALL compiler checks, however, it only relaxes a small number. For example, the compiler will still protect against uninitialized variables, full type checking will still be performed, the borrow checker will still constrain references, and many other checks will still be enforced. So what does `unsafe` actually let you do then? Only the following:

**Dereference a raw pointer:** Rather than relaxing the borrow checker rules for references, unsafe Rust instead retains them but gives unconstrained access to pointers. This is also especially important for C language interfacing.

**Call an unsafe function/method or Access fields of unions:** Examples include functions that increase performance by relaxing safety, such as by eliminating runtime range checking. Also, unsafe functions may be used as the building blocks needed in the creation of higher level abstractions (above we saw `MaybeUninit::uninit()` is an example of this). Again, this is also especially important for C language interfacing.

**Access or modify a mutable static variable:** Rust provability rules rely on local function knowledge only and since global variable usage cannot be understood without a global system usage analysis, Rust doesn't allow them in safe code.

**Inline assembler** This is needed for OS level programming,especially where access to special purpose CPU system registers is necessary.

**Implement an unsafe trait**

Refer to section [Unsafe Rust](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html) in *The Rust Programming Language* and [Unsafety](https://doc.rust-lang.org/reference/unsafety.html) in *The Rust Reference* for more rationale.

## Writing `unsafe` Code

So if `unsafe` will be necessary at times, how can you know what rules you need to keep in mind as you do it? The Rustonomicon ([https://doc.rust-lang.org/nomicon](https://doc.rust-lang.org/nomicon)), is the official document that describes what considerations are needed when writing `unsafe` code. Aside from being an interesting read with concise descriptions of the rules the compiler expects `unsafe` to abide by, it also offers examples where you might find yourself needing to use unsafe code and suggestions for ways to address it.

## Additional Considerations for `unsafe` code

**Third Party Crates/Libraries vs Unsafe**

A great strength of `cargo` and Rust crates is the wide availabilty of 3rd party libraries. However, a potential issue is the uncertain correctness of their usage of `unsafe`. While the Rust standard libraries have language experts reviewing unsafe usage (in addition to the community at large), 3rd party crates may not have such vetting.

**Coding Standards vs Unsafe**

Coding standards are a common requirement in safety-oriented development processes. They typically include both requirements and best practices to rein-in easy to misuse parts of the language. For example, one C language standard may say: "goto shall not be used to jump backwards or to create loops" while another might say "goto shall not be used at all". Similarly, in Rust, it's easy to imagine well intended limits being placed on the use of `unsafe`. However, given that `unsafe` is such an important part of the Rust provability strategy, overly draconian limitations could lead to serious problems. One area in particular where `unsafe` is absolutely necessary is interfacing to C libraries.

# Appendix B: Tension between "Machine Provable Memory Safety" and other Characteristics

Rust's overriding concern for memory safety can be at odds with other characteristics required of a project such as development velocity, system performance, prototyping, etc. For example, it's not uncommon to find that people under time pressure and struggling with the mutable aliasing rules enforced by the borrow checker, give up and accept the overhead of a reference counted pointer instead.

As a case in point, I saw the following comment on a Medium article that identifies shortcuts people can use to get around Rust's strictness with the goal of easing prototyping. From user :
> Pepitoscrespo, about a month ago: \\
> In Perl for instance, there indeed exists a no strict directive to disable strictness checks temporarily for cases like prototyping. However, Rust does not have an equivalent feature. Despite that, you can still simplify prototyping in Rust by following these points (annoying i know but it is rusty philosophy): \\
1.- Use Option or Result types for basic error handling during prototyping, instead of implementing complex error handling mechanisms. \\
2.- Utilize interior mutability with Cell, RefCell, or other similar types to avoid some borrow checker issues while prototyping. \\
3.- Prefer owned types over references to prevent dealing with lifetimes during the prototyping phase. \\
4.- Apply smart pointers like Box, Rc, or Arc (mentioned already by you) to simplify the ownership model in your prototype, helping you avoid some of the complexity of lifetimes and borrowing. \\
5.- Avoid concurrency during the initial prototyping phase to keep the code simpler, and introduce it later in the development process once the core functionality has been established.

Of course, it's easy to see how tricks like these can be applied in service of "getting things done" in general. A handy technique that makes prototyping easier may be considered a sloppy shortcut in production code. So, while on one hand, Rust offers excellent "Zero-cost abstractions", on the other hand it's strictness may also encourage shortcuts that defeat them.

Of course, shortcuts and anti-patterns exist in all languages and tend to have their own unique smells, I think the key is to simply have awareness of this potential issue and have a good code review process in place to mitigate against it.

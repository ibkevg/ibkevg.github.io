---
title: Does the need for `unsafe` mean Rust is Still a Science Project?
layout: page
---


# Rust Provability Rules vs `unsafe`

Memory safety is a such a driving design goal of the Rust language you might reasonably expect to find that the Rust standard libraries are a shining example of machine proven, memory safe, code. So, it may surprise you then to learn that not only does Rust have a Get out of Jail Free card for breaking the language safety rules, the `unsafe` keyword but the Rust standard libraries themselves contain significant amounts of `unsafe` code.

For example, bidirectional linked lists are often cited as an example of a data structure that is tricky to build both efficiently and in accordance with Rust safety rules (due in part to Rust's expectation of hierarchical data ownership, see [*Learn Rust With Entirely Too Many Linked Lists*](https://rust-unofficial.github.io/too-many-lists/)). Sure enough we find:

> rust/library/alloc/src/collections/linked_list.rs: ~1000 lines src, 59 instances of unsafe = ~16 lines per unsafe

Stepping back, we find for the rest of the standard libraries:

> rust/library/{core,std,alloc}: 128841 lines of src, 4471 instances of unsafe = 28.8 lines per unsafe

So how can a language that claims to be safe, be itself chock full of unsafe code? Is this a case of "do as I say, not as I do?"

## Rust Standard Library and unsafe wrapping

The usual purpose for a language's standard library is to provide a set of commonly needed helper routines, containers, etc. This is of course true for Rust too but Rust has an additional purpose for it's standard library: `unsafe` wrapping.

In order to prove that Rust code is correct, the Rust compiler imposes a much more strict set of rules than other languages. So much so that the strictness of these rules in practice would prevent most useful programs from being written. Thus Rust has an escape hatch, the `unsafe` keyword, that eases some of the restrictions and denotes code where the programmer is responsible for proving correctness.

It's a bit of a grand experiment really because **a big part of the Rust language development process has been to simply try writing real software within these constraints and discover cases where relaxing the rules is either necessary period or would make it easier to write software that achieves properties other than safety, such as performance.** This leads to the creation of new language features and or general purpose but safe-to-use abstractions to provide a wrapper for the necessary unsafe code. This then goes into the compiler or std library for everyone to use and is eventually considered a "stable" part of the Rust language.

See the appendix below for more thoughts on working with `unsafe` code, including 3rd Party crates and coding standards.

## A Short Example

Here is an example of the sort of thing someone coming from a language like C might run into that illustrates how the standard library first made something possible to express in Rust and years later, refined it to be fairly elegant to use.

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

Unfortunately, this won't compile because Rust does not allow an uninitialized array to be created. We could  take the path of least resistence here and just tell Rust to initialize the array with zeroes:
```
      let mut x : [[u8 ; 9] ; 9] = [[0;9];9];
```

But doing this will cause the array to be initialized twice. Let's at least *try* to be performant.  You might now decide to just wrap this in `unsafe` and move on, however, `unsafe` does not relax the variable intitialization rules, so we need to look for another solution. A short time spent googling will reveal that a std library feature called "MaybeUninit" can be applied as follows but you'll have to hold your nose:

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

Pretty gross. So we google a bit more and discover that a std lib routine, array::from_fn, was stablized in Rust 1.63 Aug/2022 to help with exactly this problem. We still have to initialize the array but we're nolonger limited to compile time constants and can instead have Rust call a function at runtime for each value as it is initialized. Using a closure, aka anonymous function, we can now write:
```
    pub fn rotate_90(&mut self) {
        let init = |r: usize, c: usize| self.grid[8 - c][r];  // init is a closure

        // Create a temporatory array that is rotated 90 degrees
        let x = array::from_fn(|r| array::from_fn(|c| init(r, c)));

        self.grid = x;
    }
```
You might notice that nowhere do we specify the size of the matrix. That's because Rust's type inference feature, figures it out automatically.

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

You can compare the assembler produced using this link: [godbolt.org](https://godbolt.org/z/7fodaWfEc). What we find is that the assembler produced by the MaybeUninit version is tighter. Perhaps this will improve as the compiler matures.

This is just one very small example of how Rust rules can lead to some sharp edges and result in software that looks very different from what you might have written in C. Also keep in mind that Rust has had three major edition releases so far: Rust 2015, Rust 2018, and Rust 2021. A project that has adopted the latest one as it's standard compiler version, Rust 2021, would find that `array::from_fn` is not be available to them. This is perhaps an argument for avoiding being too strict about locking to a specific edition, however safety critical projects that require certified compilers do not have this luxury.


# Is Rust Still a Science Project?

Rust is massively more expressive than simple languages like C. It has advanced features such as traits, generics, modules and Ada-style variant records (C union + desciminant), as well a different choices regarding basics such as type casting and copy versus move for assignment and parameter passing. For many, these features are part of the allure of Rust. However the complexity of learning and using Rust is not limited to simply understanding how best to apply these features to your software projects. Blandy et al, elegantly explain Rust's provability vs functionality strategy in their book *Programming Rust* as follows: 

>In a certain sense, Rust is less powerful than other languages: every other practical programming language lets you build arbitrary graphs of objects that point to each other in whatever way you see fit. But it is exactly because Rust is less powerful that the analyses the language can carry out on your programs can be more powerful. Rust's safety guarantees are possible exactly because the relationships it may encounter in your code are more tractable. This is part of Rust's "radical wager": in practice, Rust claims, there is usually more than enough flexibility in how one goes about solving a problem to ensure that at least a few perfectly fine solutions fall within the restrictions the language imposes.

We can now understand at least some of the complexity of using/learning Rust programming as:

  1. the need to adapt your design techniques to those that make the best of Rust's provability rules and the work arounds built into the Standard Library (thus far)
  2. distinguishing between cases that can be solved by judicious application of the standard library from cases that truly need `unsafe` will take experience. This is experience that will be hard won since the stdlib will be full of solutions to problems that you will initially not have experienced. This issue is at least mitigated by the helpful community.
  3. the tension between "machine provable memory safety" enforced by the compiler at all times and other design qualities that are not enforced by the compiler but may at times be more important such as performance or development velocity

Given that the Rust language design process is to *write software until you hit a roadblock, find a way to relax the rules and continue*, a reasonable concern when considering whether to use Rust is if the Rust community has written software similar enough to what you intend to write that you will not be getting into uncharted, science project level, territory and need to create new kinds of `unsafe` wrappers or even language features?

There's no easy answer to this short of simply doing some experiments and trying it out for yourself. 

## Examples of Known Rust Pain Points

A quick web search will reveal an enormous amount of Rust enthusiasm and advocacy, however, it's also useful to contrast this with more sober criticism.

A particularly interesting one relates to the often advertised feature of "fearless concurrency". This refers to the idea that Rust's memory safety and avoidance of data races extends to multi-threading races as well. While true, and very powerful, this fearless concurrency does not extend to [deadlocks](https://doc.rust-lang.org/book/ch16-03-shared-state.html#similarities-between-refcelltrct-and-mutextarct), because deadlocked threads are do not violate memory safety provability rules.

Another interesting limitation, is memory leaks. Similar to deadlocks, Rust provability rules do not consider a memory leak to be a memory safety issue. And while a number of useful tools are provided by Rust to aid in memory/resource management such as reference counting, leaks are still possible, for example, via [reference count cycles](https://doc.rust-lang.org/book/ch15-06-reference-cycles.html).

Rust has had three major editions so far: Rust 2015, Rust 2018, and Rust 2021. The following is an interesting analysis written in 2018 that describes many of the early pain points and refinements that were introduced to address them: [*Things Rust Doesn't Let You Do*](https://medium.com/@GolDDranks/things-rust-doesnt-let-you-do-draft-f596a3c740a5). Interestingly, a number of items that were identified then are still issues today.

More recently, in 2023 we find non-trivial pain points do still exist, consider this article: [*When Rust Hurts*](https://mmapped.blog/posts/15-when-rust-hurts.html).


## Playing to Rust's Strengths

One thing you *can* do is play to Rust's strengths and take into account how Rust's evolution has shifted focus over time as adoption increases in various application domains. Here is the glossy brochure version: [https://www.rust-lang.org/what](https://www.rust-lang.org/what)

**Command Line Tools**
Some of the earliest applications written in Rust were command line tools which I think is a reflection of Rust adoption by hobbyists. `ripgrep` is a fairly well known product of this era and it's pretty easy to find others. For example, this list is a start: [Rust Command Line Utilities](https://github.com/sts10/rust-command-line-utilities).

**Web Services**
Back-end web services were addressed in part by the introduction of `async` and associated gear. `async` is an increasingly common language feature used, for example, to reduce resource consumption by threads in large web servers. In Rust's case, adding this feature within the constraints of memory safety has been a complex ongoing effort since 2019 and is still under going refinement to reduce pain points and improve integration with the full language (e.g. async functions in traits are expected to be stabilized in 2023.) But given all this time, how mature is it and how complex is it to use? Consider this 2022 article, written by an experienced Rust programmer: [Rust Is Hard, Or: The Misery of Mainstream Programming](https://hirrolot.github.io/posts/rust-is-hard-or-the-misery-of-mainstream-programming.html). Also this: [When to use Rust and when to use Go](https://blog.logrocket.com/when-to-use-rust-when-to-use-golang)

**OS and Embedded**
Recently, the door has been opened for Rust to be used to write Linux drivers. Microsoft is doing the same: [*Microsoft is Rewriting Parts of the Windows Kernel in Rust*](https://www.thurrott.com/windows/282471/microsoft-is-rewriting-parts-of-the-windows-kernel-in-rust) This will likely lead the embedded community to drive Rust enhancements and smooth out rough edges. For a more cautious perspective on working with low level code in Rust, consider: [Rust: A Critical Retrospective](https://www.bunniestudios.com/blog/?p=6375). The following enthusiastic twitter thread about success writing a graphics driver received a fair amount of attention in the Rust community: [Lina Asahi](https://twitter.com/LinaAsahi/status/1577667445719912450). So who is right?

# Final Thoughts

As adoption by the communities in various development domains grows, so too does Rust's suitability for and usability in those domains.

If memory safety bugs form the bulk of the bugs historically in your bug tracking system or tend to be the ones that have had the most serious repercussions, as was the case for the Mozilla Firefox web browser that lead to the creation of Rust in the first place, then Rust will help you by putting it’s thumb on the scale as you code, forcing you to address these concerns as you go. The cost to you will be proveability constraints that you will be have to get used to/live with and some of these constraints will be the somewhat artificial/arbitrary consequences of the language design team not yet figuring out how to relax these constraints or not having time.

If memory safety bugs are *not* a dominant source of defects in your system, the decision becomes more complex. Adoption of Rust for business or mission critical projects should be done cautiously and with eyes wide open. Perhaps, preceded by pilot projects to evaluate whether it's pain points are serious issues in your environment or not.


# Appendix: Working with `unsafe` Code

## What does unsafe actually mean?

Many people assume that `unsafe` disables ALL compiler checks, however, it only relaxes a small number. For example, the compiler will still protect against uninitialized variables, full type checking will still be performed, the borrow checker will still constrain references, and many other checks will still be enforced. So what does `unsafe` actually let you do then?

`unsafe` allows only the following:

**Dereference a raw pointer:** Rather than relaxing the borrow checker rules for references, unsafe Rust instead retains them and instead gives unconstrained access to pointers. This is especially important for C language interfacing.

**Call an unsafe function/method or Access fields of unions:** A big use case here is interfacing to C code. Other examples include functions that provide higher performance such as by eliminating runtime range checking or providing building blocks for the creation of higher level abstractions.

**Access or modify a mutable static variable:** Rust provability rules rely on local function knowledge only and since global variable usage cannot be understood without a global system usage analysis, Rust doesn't allow them in safe code.

**Implement an unsafe trait**

Refer to section [Unsafe Rust](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html) in *The Rust Programming Language* for more rationale.

## Writing `unsafe` Code

So if `unsafe` will be necessary at times, how can you know what rules you need to keep in mind as you do it? The Rustonomicon ([https://doc.rust-lang.org/nomicon](https://doc.rust-lang.org/nomicon)), is the official document that describes what considerations are needed when writing `unsafe` code. Aside from being an interesting read with concise descriptions of the rules the compiler expects `unsafe` to abide by, it also offers examples where you might find yourself needing to use unsafe code and suggestions for ways to address it.

## Vetting `unsafe` Code

**Third Party Crates/Libraries vs Unsafe**

A great strength of `cargo` and Rust crates is the wide availabilty of 3rd party libraries. However, a potential issue is the uncertain correctness of their usage of `unsafe`. While the Rust standard libraries have language experts reviewing unsafe usage (in addition to the community at large), 3rd party crates may not have such vetting.

**Coding Standards vs Unsafe**

Coding standards are a common requirement in safety-oriented development processes. They typically include both requirements and best practices to rein-in easy to misuse parts of the language. For example, one C language standard may say: "goto shall not be used to jump backwards or to create loops" while another says "goto shall not be used at all". Similarly, in Rust, it's easy to imagine well intended limits being placed on the use of `unsafe`. However, given that `unsafe` is such an important part of the Rust provability strategy, overly draconian limitations could lead to serious problems. One area in particular where `unsafe` is absolutely necessary is interfacing to C libraries.


# Appendix

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

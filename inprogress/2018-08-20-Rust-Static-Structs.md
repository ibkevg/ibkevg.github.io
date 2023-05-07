---
title: Rust Static structs
layout: page
---


# Misc

# Static structs

Presumably the goal on the no function call constraint is to side step the static initialization problem of C++, Ada, etc. Consequences of the "can't call a function" limitation:

  1. Prevents initialization from Default::default()
  2. Prevents static data from containing most Clone types. ie. anything that would require a function call to initialize such as String (although in that specific case, replacing it with str may in some cases, be a workaround.) Basically, it's struct is limited to pointers, references and trivial Copy types.





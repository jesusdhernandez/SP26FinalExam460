# Development Log – The Torchbearer

**Student Name:** Jesus Hernandez
**Student ID:** 131481477

---

## Entry 1 – [5/14/2026]: Initial Plan

I will most likely implement select_sources first, then run_djikstra, then precompute_distances.. and go down the list in order of dependencies (e.g. precompute requires djikstra's, so implement djikstra's first). 
I expect proving invariance to be the most difficult because I struggle with proofs, alongside brainstorming how to implement certain functions to be difficult (especially pruning). 
I plan to test this by creating maps that have ideal pathing options, non-ideal pathing options, as well as abysmal pathing options between important nodes, and then running the completed functions against those and comparing them against my hand traced solutions.

---

## Entry 2 – [5/14/2026]: README completed

I've just completed the README and am about to start implementing the functions in Python. I think I have a good idea of how I want to design the program in details, e.g. how I will pathfind to each location. I am still a bit unsure as to how exactly I want to go about combining these with pruning and overall pathfinding.

---

## Entry 3 – [5/14/2026]: Progress Implementing Python Functions

So far, things have been mostly smooth sailing. One minor annoyance is that I almost forgot to remove duplicates from select_sources. I kind of used a janky fix where I just made it into a set, and then back into a list... and it somehow works! 
It also is taking me a while to figure out how exactly to implement the remaining functions, such as `_explore`, and it is getting pretty close to the deadline.

---

## Entry 4 – [5/14/2026]: Post-Implementation Reflection

After writing my implementation, I realized that I entirely forgot to leave comments explaining my work. I'm quite worried about it in my grade, since it is in the rubric.. oops :(. I think my functions should work correctly, though, as the given tests passed. If given more time, I definitely would have added explanatory comments, and I would probably study edge cases a lot closer.

This semester has honestly been such a trainwreck for me, and I'm really glad it's finally over. I am so mentally exhausted I cannot put it into words.

---

(Edit 5/15: I don't know if it bugged or if I forgot to commit it, but this is a bogus edit merely to get Git to recognize a "change" in this file so it pushes my finished devlog this time. Thank you!)
## Final Entry – [5/14/2026]: Time Estimate

| Part                           | Estimated Hours |
| ------------------------------ | --------------- |
| Part 1: Problem Analysis       | 0.4             |
| Part 2: Precomputation Design  | 1.3             |
| Part 3: Algorithm Correctness  | 2.1             |
| Part 4: Search Design          | 0.3             |
| Part 5: State and Search Space | 1.4             |
| Part 6: Pruning                | 0.9             |
| Part 7: Implementation         | 0.8             |
| README and DEVLOG writing      | 6.1             |
| **Total**                      | 13.3            |

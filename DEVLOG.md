# Development Log – The Torchbearer

**Student Name:** William Kate IV
**Student ID:** 827900522

> Instructions: Write at least four dated entries. Required entry types are marked below.
> Two to five sentences per entry is sufficient. Write entries as you go, not all in one
> sitting. Graders check that entries reflect genuine work across multiple sessions.
> Delete all blockquotes before submitting.

---

## Entry 1 – [May 9th, 2026]: Initial Plan

> Required. Write this before writing any code. Describe your plan: what you will
> implement first, what parts you expect to be difficult, and how you plan to test.

I plan to start by implementing Dijkstra's algorithm first since I need to figure out the shortest paths between the important nodes. After doing that, I will do a precomputation for the distances betweeen S, all of the relics nodes, and T so that I can have something that is a smaller graph. I think the main challenge I will face will be figuring out the best order to visit all the relics since there are many different path combinations to try. Specifically, the search part that involves pruning and backtracking will most likely be the hardest thing for me to figure out and implement. To test everything, I will start with smaller graphs where I can confirm the optimal path manually and then from there expand and try more difficult cases until everything works.

---

## Entry 2 – [May 11th, 2026]: [Understanding Dijkstra Correctness and Design]

Today I workd on Part 3 and focused on understanding why Dijkstra's algorithm produces correct shortest-path distances, especially the invariant involving finalized and non-finalized nodes. I worked through how the algorithm maintains correctness at each step and why nonnegative edge weights are important for ensuring the minimum-distance node is always safe to finalize. I also spent time organizing the precomputation design and making sure I understood how the distance table will be user later on in the search. This was able to help me clairfy how all the parts fit together before moving on to implementing the next section.

---

## Entry 3 – [May 12th, 2026]: [Search Design and Recursive Implementation]

> Required. At least one entry must describe a bug, wrong assumption, or design change
> you encountered. Describe what went wrong and how you resolved it.

Today I worked on designing the search algorithm and implementing the recursive exploration for finding the optimal route. I focused on understanding why a greedy approach fails and how the algorithm must consider different orders of visiting relics, which led me to implementing a brute-force recursive solution with backtracking. While testing, I ran into a bug where my function was returning a suboptimal path, and I initially thought my distance table was wrong. After debugging, I realized the issue was due to incorrect indentation in my recursive function, which caused the backtracking step to not run properly. Fixing the indentation ensured all possible paths were explored and the correct minimum cost was found.

---

## Entry 4 – [Date]: Post-Implementation Reflection

> Required. Written after your implementation is complete. Describe what you would
> change or improve given more time.

_Your entry here._

---

## Final Entry – [Date]: Time Estimate

> Required. Estimate minutes spent per part. Honesty is expected; accuracy is not graded.

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | 30 minutes |
| Part 2: Precomputation Design | 1.5 hours |
| Part 3: Algorithm Correctness | 1 hour |
| Part 4: Search Design | 1 hour |
| Part 5: State and Search Space | 2.5 hours |
| Part 6: Pruning | |
| Part 7: Implementation | |
| README and DEVLOG writing | |
| **Total** | |

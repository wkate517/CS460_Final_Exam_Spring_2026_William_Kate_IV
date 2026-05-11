# The Torchbearer

**Student Name:** William Kate IV
**Student ID:** 827900522
**Course:** CS 460 – Algorithms | Spring 2026

> This README is your project documentation. Write it the way a developer would document
> their design decisions , bullet points, brief justifications, and concrete examples where
> required. You are not writing an essay. You are explaining what you built and why you built
> it that way. Delete all blockquotes like this one before submitting.

---

## Part 1: Problem Analysis

> Document why this problem is not just a shortest-path problem. Three bullet points, one
> per question. Each bullet should be 1-2 sentences max.

- **Why a single shortest-path run from S is not enough:**

- Running a single shortest-path algorithm from S only tells us the cheapest way to reach each node individually, it doesn't tell us the best order to visit all the relics.

- **What decision remains after all inter-location costs are known:**

- Even if we know the shortest distances between every pair of important nodes, we still have to decide the order in which to visit the relics before going to T.

- **Why this requires a search over orders (one sentence):**

- This problem is really about trying different orders of visiting relics since the total cost changes depending on the order, so it is not just one shortest path calculation.

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

> List the source node types as a bullet list. For each, one-line reason.

| Source Node Type | Why it is a source |
|---|---|
| Start node (S) | Need to compute the shortest paths from the start node, then to all relics, and then to T.|
| Relic nodes (M) | Need to compute the shortest paths between each relic and then ultimately to T. |

### Part 2b: Distance Storage

> Fill in the table. No prose required.

| Property | Your answer |
|---|---|
| Data structure name | Dictionary (hash map) |
| What the keys represent | Pair of nodes (u, v) where u and v are important nodes |
| What the values represent | Shortest distance of path from node u to node v |
| Lookup time complexity | O(1)|
| Why O(1) lookup is possible | A dictionary uses hashing to access values by key directly |

### Part 2c: Precomputation Complexity

> State the total complexity and show the arithmetic. Two to three lines max.

- **Number of Dijkstra runs:** k + 2
- **Cost per run:** O(m log n)
- **Total complexity:** O((k + 2) m log n)
- **Justification (one line):** Dijkstra's is run once from S, then again once from T, and then once from each of the k relic nodes.

---

## Part 3: Algorithm Correctness

> Document your understanding of why Dijkstra produces correct distances.
> Bullet points and short sentences throughout. No paragraphs.

### Part 3a: What the Invariant Means

> Two bullets: one for finalized nodes, one for non-finalized nodes.
> Do not copy the invariant text from the spec.

- **For nodes already finalized (in S):**
- Once a node has been finalized, it's associated distance value is set because Dijkstra's algorithm has already found the cheapest possible path to it.

- **For nodes not yet finalized (not in S):**
- These nodes that have not yet been finalized still have their temporary distance estimates based on the best possible paths that have been discovered so far, and the estimates may improve as more edges are explored.

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
- Initially, only the source node has a distance that is 0 and all the other nodes are set to infinity, so the invariant holds because no paths that are incorrect have been considered yet.

- **Maintenance : why finalizing the min-dist node is always correct:**
- When picking the node with the smallest distance it must be correct because all the edge weights are nonnegative, so there is no way a shorter path to it can be found later on.

- **Termination : what the invariant guarantees when the algorithm ends:**
- When the algorithm terminates, all the nodes are finalized, so the invariant guarantees that every distance value is the true shortest path from the source.

### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

- Having accurate shortest-path distances ensures that the route planner selects the most efficient path for reaching all the relics and then eventually reaching the exit.

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** _Your answer here._
- **Counter-example setup:** _Your answer here._
- **What greedy picks:** _Your answer here._
- **What optimal picks:** _Your answer here._
- **Why greedy loses:** _Your answer here._

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- _Your answer here._

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | | | |
| Relics already collected | | | |
| Fuel cost so far | | | |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | |
| Operation: check if relic already collected | Time complexity: |
| Operation: mark a relic as collected | Time complexity: |
| Operation: unmark a relic (backtrack) | Time complexity: |
| Why this structure fits | |

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** _Your answer (in terms of k)._
- **Why:** _One-line justification._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** _Your answer here._
- **When it is used:** _Your answer here._
- **What it allows the algorithm to skip:** _Your answer here._

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** _Your answer here._
- **What the lower bound accounts for:** _Your answer here._
- **Why it never overestimates:** _Your answer here._

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Your answer here._

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Your references here._

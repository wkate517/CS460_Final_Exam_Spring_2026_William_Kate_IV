# The Torchbearer

**Student Name:** William Kate IV
**Student ID:** 827900522
**Course:** CS 460 – Algorithms | Spring 2026

---

## Part 1: Problem Analysis

- **Why a single shortest-path run from S is not enough:**

- Running a single shortest-path algorithm from S only tells us the cheapest way to reach each node individually, it doesn't tell us the best order to visit all the relics.

- **What decision remains after all inter-location costs are known:**

- Even if we know the shortest distances between every pair of important nodes, we still have to decide the order in which to visit the relics before going to T.

- **Why this requires a search over orders (one sentence):**

- This problem is really about trying different orders of visiting relics since the total cost changes depending on the order, so it is not just one shortest path calculation.

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

| Source Node Type | Why it is a source |
|---|---|
| Start node (S) | Need to compute the shortest paths from the start node, then to all relics, and then to T.|
| Relic nodes (M) | Need to compute the shortest paths between each relic and then ultimately to T. |

### Part 2b: Distance Storage

| Property | Your answer |
|---|---|
| Data structure name | Dictionary (hash map) |
| What the keys represent | Pair of nodes (u, v) where u and v are important nodes |
| What the values represent | Shortest distance of path from node u to node v |
| Lookup time complexity | O(1)|
| Why O(1) lookup is possible | A dictionary uses hashing to access values by key directly |

### Part 2c: Precomputation Complexity

- **Number of Dijkstra runs:** k + 2
- **Cost per run:** O(m log n)
- **Total complexity:** O((k + 2) m log n)
- **Justification (one line):** Dijkstra's is run once from S, then again once from T, and then once from each of the k relic nodes.

---

## Part 3: Algorithm Correctness

### Part 3a: What the Invariant Means

- **For nodes already finalized (in S):**
- Once a node has been finalized, it's associated distance value is set because Dijkstra's algorithm has already found the cheapest possible path to it.

- **For nodes not yet finalized (not in S):**
- These nodes that have not yet been finalized still have their temporary distance estimates based on the best possible paths that have been discovered so far, and the estimates may improve as more edges are explored.

### Part 3b: Why Each Phase Holds

- **Initialization : why the invariant holds before iteration 1:**
- Initially, only the source node has a distance that is 0 and all the other nodes are set to infinity, so the invariant holds because no paths that are incorrect have been considered yet.

- **Maintenance : why finalizing the min-dist node is always correct:**
- When picking the node with the smallest distance it must be correct because all the edge weights are nonnegative, so there is no way a shorter path to it can be found later on.

- **Termination : what the invariant guarantees when the algorithm ends:**
- When the algorithm terminates, all the nodes are finalized, so the invariant guarantees that every distance value is the true shortest path from the source.

### Part 3c: Why This Matters for the Route Planner

- Having accurate shortest-path distances ensures that the route planner selects the most efficient path for reaching all the relics and then eventually reaching the exit.

---

## Part 4: Search Design

### Why Greedy Fails

- **The failure mode:** A greedy approach always picks the nearest next relic, but that choice can lead to a total path that is worse because it doesn't consider the future costs.
- **Counter-example setup:** Assume that from S distances are: S to B = 1, S to C = 2, and S to D = 2, however traveling between relics is uneven (ex: B to C is very expensive but C to B is cheap).
- **What greedy picks:** Greedy would pick relic B first because it has the smallest distance from S. 
- **What optimal picks:** Optimal would pick either relic C or D to avoid the expensive path that comes after choosing B.
- **Why greedy loses:** By choosing B first the next step would be very costly, even though it was optimal at the time, it leads to a higher total cost than choosing a different order of relics.

### What the Algorithm Must Explore

- The algorithm must explore different orderings of visiting relics because the overall total cost is dependent on the order in which they are visited.

---

## Part 5: State and Search Space

### Part 5a: State Representation

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | current_loc | node | The node where the search path is currently located |
| Relics already collected | relics_visited_order | list[node] | The ordered list of relics that have been visited so far |
| Fuel cost so far | cost_so_far | float | The total fuel cost that has been accumulated up to the current state |

### Part 5b: Data Structure for Visited Relics

| Property | Your answer |
|---|---|
| Data structure chosen | set |
| Operation: check if relic already collected | Time complexity: O(1) |
| Operation: mark a relic as collected | Time complexity: O(1) |
| Operation: unmark a relic (backtrack) | Time complexity: O(1) |
| Why this structure fits | This structure fits because it allows us to quickly check if a relic has been collected and efficiently add or remove it during the search |

### Part 5c: Worst-Case Search Space

- **Worst-case number of orders considered:** k!
- **Why:** In the worst case the algorithm would have to try every possible ordering of k relics to find the optimal route.

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

- **What is tracked:** The algorithm keeps track of the current minimum, the best, total fuel cost found so far also with the corresposponding order of visited relics.
- **When it is used:** It is used during the search before continuing deeper into recurstion so that it can compare the current path's cost to the best known solution.
- **What it allows the algorithm to skip:** It allows the algorithm to skip exploring any of the paths where the current cost is already greater than or equal to the best cost that has been found so far.

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** The algorithm knows the current location, the relics remaining, the relics that have been visited, and the total cost found so far.
- **What the lower bound accounts for:** The lower bound accounts for the current cost that has been found so far and an estimate of the minimum cost that is possible to achieve when visiting the remaining relics and then reach the exit.
- **Why it never overestimates:** It never overestimates because it only uses the shortest-path distances that are found in the precomputed table.

### Part 6c: Pruning Correctness

- If a path that is being developed already has a cost that is worse than the best solution that has been found so far, then there is no reason to keep exploring because it can't improve the result.

- Because all of the costs are nonnegative, adding more edges will only increase the total cost.

---

## References

- Lecture Notes

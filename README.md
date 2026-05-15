# The Torchbearer

**Student Name:** Jesus Hernandez
**Student ID:** 131481477
**Course:** CS 460 – Algorithms | Spring 2026

---
## Part 1: Problem Analysis

- **Why a single shortest-path run from S is not enough:**
  A single shortest-path run from S is not enough because we must also visit each M (relic chambers) on the way to T. 

- **What decision remains after all inter-location costs are known:**
  After all inter-location costs are known, we must still decide which path to take to get to each M and then to T. 

- **Why this requires a search over orders (one sentence):**
  This requires a search over orders because we don't know which relic chamber to visit first.

---
## Part 2: Precomputation Design

### Part 2a: Source Selection

| Source Node Type  | Why it is a source                                                                                     |
| ----------------- | ------------------------------------------------------------------------------------------------------ |
| S (start)         | This is where we start from, it is the definition of a source                                          |
| M (relic chamber) | Once we visit a relic chamber, we have to continue the path, so this is also a source to continue from |

### Part 2b: Distance Storage

| Property                  | Your answer                                                                                                                                            |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Data structure name       | Nested hashmap (nested dictionary in Python?)                                                                                                          |
| What the keys represent   | Start and Target nodes, e.g. S and T = `['S']['T']`, respectively                                                                                      |
| What the values represent | Since there's only one shortest distance needed to be kept between each pair of nodes, no conflicts should exist in the hashmaps, thus keeping it O(1) |

### Part 2c: Precomputation Complexity

- **Number of Dijkstra runs:** k + 1, where k = |M|
- **Cost per run:** O(m log n)
- **Total complexity:** O(k m log n)
- **Justification (one line):** It is ran k + 1 times, but simplifying for big O drops the +1.

---

## Part 3: Algorithm Correctness

### Part 3a: What the Invariant Means

- **For nodes already finalized (in S):**
  Each of the nodes in S have been finalized, which means that their minimum distances have already been found. Because every other possible value must be larger than the minimum, the algorithm cannot find any smaller value.

- **For nodes not yet finalized (not in S):**
  Each of the nodes not in S are processed from a finalized node, which means that finding the minimum distance to a non-finalized node from the finalized node is also the minimum distance overall, thus finalizing the node.

### Part 3b: Why Each Phase Holds

- **Initialization : why the invariant holds before iteration 1:**
  The invariant holds before iteration 1 because we haven't yet finalized nor looked at any node distances besides our source, and since the distance to the source from the source is always 0, the invariant holds.

- **Maintenance : why finalizing the min-dist node is always correct:**
  Finalizing the min-dist node is always correct because since it is the minimum/shortest path, and all other weights are nonnegative, no other shorter path can possibly exist. 

- **Termination : what the invariant guarantees when the algorithm ends:**
  The invariant guarantees that all distances to all nodes from the starting node are the minimum distances.

### Part 3c: Why This Matters for the Route Planner

This matters for the route planner because the route must have the minimum cost getting from S to T, so having the minimum distances to each node is crucial for knowing which path to take.

---

## Part 4: Search Design

### Why Greedy Fails

- **The failure mode:** Torchbearer either never finds the exit, or chooses a non-optimal path and wastes fuel.
- **Counter-example setup:** S -> A -> B -> C -> D -> T with a distance of 1 each, while S -> E -> T with a distance of 2 each.
- **What greedy picks:** S -> A -> B -> C -> D -> T
- **What optimal picks:** S -> E -> T
- **Why greedy loses:** Since each edge from S to A to T has a cost of 1, we have a total cost of 1 + 1 + 1 + 1 + 1 = 5, while S -> E -> T has a distance of 2 + 2 = 4. Thus, greedy has a higher cost than the optimal path.

### What the Algorithm Must Explore

- The algorithm must explore the most optimal order of relic chambers to visit. 

---
## Part 5: State and Search Space

### Part 5a: State Representation

| Component                | Variable name in code | Data type | Description                                |
| ------------------------ | --------------------- | --------- | ------------------------------------------ |
| Current location         | curr                  | node      | The node the torchbearer is currently at   |
| Relics already collected | visited               | list      | A list of already visited/collected relics |
| Fuel cost so far         | cost                  | float     | A sum of fuel cost as a number             |
### Part 5b: Data Structure for Visited Relics

| Property                                    | Your answer                                                                      |
| ------------------------------------------- | -------------------------------------------------------------------------------- |
| Data structure chosen                       | list                                                                             |
| Operation: check if relic already collected | Time complexity: O(n)                                                            |
| Operation: mark a relic as collected        | Time complexity: O(1)                                                            |
| Operation: unmark a relic (backtrack)       | Time complexity: O(1)                                                            |
| Why this structure fits                     | It fits because we're keeping a list of visited relics, without a specific order |
### Part 5c: Worst-Case Search Space

- **Worst-case number of orders considered:** $k^2$
- **Why:** For each M, we are comparing the distance to each M and exit, thus making it $|M|\times|M|=k\times k=k^2$

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

- **What is tracked:** the shortest distance to each room, from each room.
- **When it is used:** when determining the order of which chambers to visit
- **What it allows the algorithm to skip:** non-optimal paths to each chamber, as well as paths to irrelevant rooms.

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** _Your answer here._
- **What the lower bound accounts for:** _Your answer here._
- **Why it never overestimates:** _Your answer here._

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Your answer here._

---

## References

> Bullet list. If none beyond lecture notes, write that.

- None beyond lectures

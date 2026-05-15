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

| Property                  | Your answer                                                                                                                                                             |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Data structure name       | Nested hashmap (nested dictionary in Python?)                                                                                                                           |
| What the keys represent   | Start and Target nodes, e.g. S and T = `['S']['T']`, respectively                                                                                                       |
| What the values represent | Since there's only one shortest distance needed to be kept between each pair of nodes, no conflicts should exist in the hashmaps, thus keeping it O(1)                  |
| Lookup time complexity    | O(1)                                                                                                                                                                    |
| Why O(1) is achievable    | It is achievable because since all nodes can only have one shortest path (if there are ties, we only pick one), there are no conflicts in the map, thus achieving O(1). |

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
  For nodes not yet finalized, their distance values are the best we have found so far through finalized nodes, so these values could decrease later on if a shorter path is found. Once a minimum distance is found from a finalized node, it is then finalized itself.

### Part 3b: Why Each Phase Holds

- **Initialization : why the invariant holds before iteration 1:**
  The invariant holds before iteration 1 because we haven't yet finalized nor looked at any node distances besides our source, and since the distance to the source from the source is always 0, the invariant holds.

- **Maintenance : why finalizing the min-dist node is always correct:**
  Finalizing the min-dist node is always correct because since it is the minimum/shortest path, and all other weights are nonnegative (thus an existing path cannot have its distance shortened later on), no other shorter path can possibly exist. 

- **Termination : what the invariant guarantees when the algorithm ends:**
  The invariant guarantees that all distances to all nodes from the starting node are the minimum distances.

### Part 3c: Why This Matters for the Route Planner

This matters for the route planner because the route must have the minimum cost getting from S to T, so having the minimum distances to each node is crucial for knowing which path to take.

---

## Part 4: Search Design

### Why Greedy Fails

- **The failure mode:** Torchbearer either never finds the exit, or chooses a non-optimal path and wastes fuel.
- **Counter-example setup:**

| From \ To | B   | C   | D   | T   |
| --------- | --- | --- | --- | --- |
| S         | 1   | 2   | 2   | -   |
| B         | -   | 4   | 3   | 7   |
| C         | 1   | -   | 1   | 10  |
| D         | 45  | 24  | -   | 3   |

- **What greedy picks:** S -> B -> D -> C -> T
- **What optimal picks:** S -> C -> B -> D -> T
- **Why greedy loses:** Since B is the most immediate relic chamber available from S, it picks it. However, the options from there are more expensive than the options at C, which costs it more already, and this continues until we reach T.
### What the Algorithm Must Explore

- The algorithm must explore the most optimal order of relic chambers to visit. 

---
## Part 5: State and Search Space

### Part 5a: State Representation

| Component                | Variable name in code | Data type | Description                                         |
| ------------------------ | --------------------- | --------- | --------------------------------------------------- |
| Current location         | current_loc           | node      | The node the path currently ends at                 |
| Relics already collected | relics_visited_order  | list      | An ordered list of already visited/collected relics |
| Fuel cost so far         | cost_so_far           | float     | A sum of fuel cost as a number                      |
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
- **Why:** For each M, we are comparing the distance to each leftover M and exit, thus making it $|M|\times|M|=k\times k=k^2$

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

- **What is tracked:** the cheapest route found so far, as well as the order.
- **When it is used:** when determining the order of which chambers to visit
- **What it allows the algorithm to skip:** non-optimal paths (i.e. more expensive ones than what's already known)

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** current location, chambers remaining, cost thus far, and the cost to next room options.
- **What the lower bound accounts for:** current cost / minimum amount of cost to the path.
- **Why it never overestimates:** it never overestimates because all future edges can only add on to the cost as all weights are nonnegative, thus making this a minimum.

### Part 6c: Pruning Correctness

- Pruning is safe because if we've found the cheapest path to take, the other paths must cost more to take. Thus, they are not worth keeping as they can only further increase in cost.

---

## References

- None beyond lectures

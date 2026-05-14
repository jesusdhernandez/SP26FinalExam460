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
| Data structure name       | Nested hashmap (nested dictionary in Python?                                                                                                           |
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

> Two bullets: one for finalized nodes, one for non-finalized nodes.
> Do not copy the invariant text from the spec.

- **For nodes already finalized (in S):**
  Each of the nodes in S have been finalized, which means that their minimum distances have already been found. Because every other possible value must be larger than the minimum, the algorithm cannot find any smaller value. 

- **For nodes not yet finalized (not in S):**
  Each of the nodes not in S are processed from a finalized node, 

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
  _Your answer here._

- **Maintenance : why finalizing the min-dist node is always correct:**
  _Your answer here._

- **Termination : what the invariant guarantees when the algorithm ends:**
  _Your answer here._

### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

_Your answer here._

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

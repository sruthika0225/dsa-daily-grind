# Day 12 — Climbing Stairs

**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** Dynamic Programming · Recursion · Memoization

---

## Problem Statement

You are climbing a staircase that has `n` steps.

Each time, you can either climb:

- 1 step
- 2 steps

Return the number of **distinct ways** to reach the top.

---

### Example 1

**Input**

```text
n = 2
```

**Output**

```text
2
```

**Explanation**

There are two possible ways:

```text
1 + 1
2
```

---

### Example 2

**Input**

```text
n = 3
```

**Output**

```text
3
```

**Explanation**

There are three possible ways:

```text
1 + 1 + 1
1 + 2
2 + 1
```

---

## ✅ Approach — Recursion with Memoization (Accepted)

```python
class Solution:
    def climbStairs(self, n: int, mem={}) -> int:
        if mem.get(n):
            return mem.get(n)

        if n <= 2:
            return n

        mem[n] = self.climbStairs(n - 1, mem) + self.climbStairs(n - 2, mem)

        return mem[n]
```

---

## Idea

At every step, there are only two possible choices:

- Take **1 step**
- Take **2 steps**

So, the total number of ways to reach step `n` is:

```text
Ways(n) = Ways(n - 1) + Ways(n - 2)
```

This is because:

- If the last move was **1 step**, we must have come from `n - 1`.
- If the last move was **2 steps**, we must have come from `n - 2`.

To avoid recalculating the same subproblems repeatedly, we store previously computed answers in a dictionary (`mem`).

---

## Dry Run

### Input

```text
n = 5
```

Recursive calls:

```text
Ways(5)
│
├── Ways(4)
│   ├── Ways(3)
│   │   ├── Ways(2) = 2
│   │   └── Ways(1) = 1
│   │
│   └── Ways(2) = 2
│
└── Ways(3)
    (Already stored in memo)
```

Memoization table:

| n | Ways |
|---|------|
|1|1|
|2|2|
|3|3|
|4|5|
|5|8|

Answer:

```text
8
```

---

## Why Memoization?

Without memoization, the recursive tree repeatedly computes the same values.

Example:

```text
Ways(5)
├── Ways(4)
│   └── Ways(3)
└── Ways(3)
```

Notice that `Ways(3)` is calculated multiple times.

Using a memo dictionary:

```python
mem[n]
```

Once a value has been computed, it is stored and reused whenever needed.

This significantly improves efficiency.

---

## Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Time | O(n) |
| Extra Space | O(n) |

where:

- `n` is the number of stairs.

Each value from `1` to `n` is computed only once.

---

## Constraints

- `1 ≤ n ≤ 45`

---

## Key Takeaway

This problem is a classic example of **Dynamic Programming**.

The recurrence relation:

```text
Ways(n) = Ways(n-1) + Ways(n-2)
```

is identical to the Fibonacci sequence.

Using **memoization**, we eliminate repeated recursive calls and reduce the time complexity from **O(2ⁿ)** to **O(n)**.

> **Whenever a recursive problem contains overlapping subproblems, memoization is a powerful optimization technique that transforms an exponential solution into a linear one.**

# Day 04 — Kth Smallest Element

**Platform:** GeeksforGeeks  
**Difficulty:** Medium | **Accuracy:** 35.17% | **Points:** 4  
**Topic:** Arrays · Sorting · Order Statistics

---

## Problem Statement

Given an integer array `arr[]` and an integer `k`, find and return the kth smallest element in the array based on sorted order.

```
Input:  arr = [10, 5, 4, 3, 48, 6, 2, 33, 53, 10], k = 4
Output: 5
```
```
Input:  arr = [7, 10, 4, 3, 20, 15], k = 3
Output: 7
```

**Sorted view:**
```
[10, 5, 4, 3, 48, 6, 2, 33, 53, 10]
 →  [2, 3, 4, 5, 6, 10, 10, 33, 48, 53]
              ↑
            k=4 → 5
```

---

## Approaches

### ❌ Approach 1 — Repeated Min Removal (TLE)

```python
class Solution:
    def kthSmallest(self, arr, k):
        for i in range(k - 1):
            arr.pop(arr.index(min(arr)))
        return min(arr)
```

**Idea:** Remove the minimum element `k-1` times. Whatever remains as the minimum is the answer.

**Why it TLEs:**

Each iteration runs three separate O(n) operations:

| Operation | Cost |
|-----------|------|
| `min(arr)` | O(n) |
| `arr.index(...)` | O(n) |
| `arr.pop(...)` | O(n) — list shift |

Stacked over `k-1` iterations → **O(k × n)** → worst case **O(n²)**  
For `n = 10^5`, that's up to **10 billion operations**. TLE is inevitable.

---

### ✅ Approach 2 — Sort (Accepted)

```python
class Solution:
    def kthSmallest(self, arr, k):
        arr.sort()
        return arr[k - 1]
```

**Idea:** Sort the array. The kth smallest is directly at index `k-1`.

| | |
|--|--|
| Time | O(n log n) — Python's Timsort |
| Space | O(1) — in-place |

Once sorted, the answer is a single index lookup. Clean, readable, accepted.

---

## Constraints

- `1 ≤ arr.size() ≤ 10^5`
- `1 ≤ arr[i] ≤ 10^5`
- `1 ≤ k ≤ arr.size()`

---

## Key Takeaway

> Calling `min()` inside a loop is a hidden O(n) scan every single iteration.
> That's what turned a simple idea into an O(n²) TLE.
> Sorting upfront pays the cost once — and makes every lookup O(1) after.

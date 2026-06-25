# Day 08 — Remove Element

**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** Array · Two Pointers · In-Place Modification

---

## Problem Statement

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` **in-place**.

The order of the remaining elements may be changed.

Return the number of elements that are **not equal** to `val`.

The first `k` elements of `nums` should contain the elements not equal to `val`, where `k` is the number of remaining elements.

---

### Example 1

**Input**

```text
nums = [3,2,2,3]
val = 3
```

**Output**

```text
2, nums = [2,2,_,_]
```

**Explanation**

After removing all `3`s, the remaining elements are:

```text
[2,2]
```

---

### Example 2

**Input**

```text
nums = [0,1,2,2,3,0,4,2]
val = 2
```

**Output**

```text
5, nums = [0,1,4,0,3,_,_,_]
```

**Explanation**

After removing all `2`s, the first five elements contain:

```text
[0,0,1,3,4]
```

The order does not matter.

---

## ✅ Approach — Swap with Last Element (Accepted)

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        itr = 0
        total = len(nums)

        while itr < total:
            if nums[itr] == val:
                nums[itr] = nums[total - 1]
                total -= 1
            else:
                itr += 1

        return total
```

---

## Idea

Since the order of the remaining elements **does not matter**, we can avoid shifting elements.

Instead:

- Traverse the array using an index `itr`.
- Whenever `val` is found:
  - Replace it with the last valid element.
  - Reduce the effective array size (`total`).
- Do **not** increment `itr` immediately because the swapped element hasn't been checked yet.
- If the current element is not `val`, simply move to the next index.

This efficiently removes unwanted elements in-place.

---

## Dry Run

```text
nums = [3,2,2,3]
val = 3

itr = 0
total = 4
```

| Step | Array | itr | total |
|------|-------|-----|-------|
|Initial|[3,2,2,3]|0|4|
|3 found → swap with last|[3,2,2,3]|0|3|
|3 found again → swap with last valid|[2,2,2,3]|0|2|
|2 != 3|[2,2,2,3]|1|2|
|2 != 3|[2,2,2,3]|2|2|

Loop ends.

Answer:

```text
k = 2

First two elements:
[2,2]
```

---

## Why This Works

Unlike the previous problem (**Remove Duplicates from Sorted Array**), this problem **does not require preserving the order** of the remaining elements.

Because of this, replacing the current element with the last valid element avoids expensive shifting operations.

After each swap:

- One unwanted element is removed.
- The valid portion of the array becomes one element shorter.
- Every remaining element is checked exactly once.

---

## Complexity Analysis

| Operation | Complexity |
|------------|------------|
| Traversal | O(n) |
| Extra Space | O(1) |

where:

- `n = len(nums)`

---

## Constraints

- `0 ≤ nums.length ≤ 100`
- `0 ≤ nums[i] ≤ 50`
- `0 ≤ val ≤ 100`

---

## Key Takeaway

Whenever **element order doesn't matter**, swapping an unwanted element with the last valid element is often more efficient than shifting all subsequent elements.

This technique:

- Removes elements in-place
- Uses constant extra space
- Runs in linear time

> **Understanding the problem constraints can lead to simpler and more efficient solutions. Here, ignoring the order allows us to use a clever swap-based approach instead of shifting elements.**

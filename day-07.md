# Day 07 — Remove Duplicates from Sorted Array

**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** Arrays · Two Pointers · In-Place Modification

---

## Problem Statement

Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once.

The relative order of the elements should remain the same.

Return the number of unique elements `k`.

The first `k` elements of `nums` should contain the unique values in sorted order. Elements beyond index `k - 1` can be ignored.

---

### Example 1

**Input**

```text
nums = [1,1,2]
```

**Output**

```text
2, nums = [1,2,_]
```

**Explanation**

After removing duplicates, the first two elements are:

```text
[1,2]
```

The remaining elements can be anything.

---

### Example 2

**Input**

```text
nums = [0,0,1,1,1,2,2,3,3,4]
```

**Output**

```text
5, nums = [0,1,2,3,4,_,_,_,_,_]
```

**Explanation**

The unique elements are:

```text
[0,1,2,3,4]
```

---

## ✅ Approach — Two Pointers (Accepted)

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        prev = nums[0]
        next_index = 1

        for itr in range(1, len(nums)):
            if nums[itr] != prev:
                nums[next_index] = nums[itr]
                next_index += 1
                prev = nums[itr]

        return next_index
```

---

## Idea

Since the array is already sorted, duplicate elements appear consecutively.

We can maintain:

- `prev` → previous unique element seen.
- `next_index` → position where the next unique element should be placed.

Whenever a new element different from `prev` is encountered:

1. Place it at `nums[next_index]`.
2. Increment `next_index`.
3. Update `prev`.

At the end, `next_index` equals the number of unique elements.

---

## Dry Run

```text
nums = [0,0,1,1,1,2,2,3,3,4]

prev = 0
next_index = 1
```

| i | nums[i] | Different from prev? | Array after operation | next_index |
|---|---------|----------------------|----------------------|------------|
|1|0|No|[0,0,1,1,1,2,2,3,3,4]|1|
|2|1|Yes|[0,1,1,1,1,2,2,3,3,4]|2|
|3|1|No|[0,1,1,1,1,2,2,3,3,4]|2|
|4|1|No|[0,1,1,1,1,2,2,3,3,4]|2|
|5|2|Yes|[0,1,2,1,1,2,2,3,3,4]|3|
|6|2|No|[0,1,2,1,1,2,2,3,3,4]|3|
|7|3|Yes|[0,1,2,3,1,2,2,3,3,4]|4|
|8|3|No|[0,1,2,3,1,2,2,3,3,4]|4|
|9|4|Yes|[0,1,2,3,4,2,2,3,3,4]|5|

Final answer:

```text
k = 5
nums = [0,1,2,3,4,...]
```

---

## Why This Works

Because the array is sorted:

```text
Duplicates always appear next to each other.
```

Therefore, comparing each element with the previous unique element is enough to detect duplicates.

The unique values are continuously packed into the beginning of the array.

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

- `1 ≤ nums.length ≤ 3 × 10⁴`
- `-100 ≤ nums[i] ≤ 100`
- `nums` is sorted in non-decreasing order.

---

## Key Takeaway

When an array is already sorted, duplicates become adjacent. Instead of using an additional data structure like a set, we can use two pointers:

- One pointer scans the array.
- The other keeps track of where the next unique element should go.

This allows us to remove duplicates **in-place** with:

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

> **Sorted arrays often allow us to solve problems efficiently using the Two Pointer technique without extra memory.**

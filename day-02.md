# 167. Two Sum II - Input Array Is Sorted

**Difficulty:** Medium
**Link:** https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

## Problem

Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.

### Examples

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2.

Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3.

Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2.
```

### Constraints

- `2 <= numbers.length <= 3 * 10^4`
- `-1000 <= numbers[i] <= 1000`
- `numbers` is sorted in non-decreasing order.
- `-1000 <= target <= 1000`
- The tests are generated such that there is exactly one solution.

## Approach: Two Pointers

Since the array is already sorted, a two-pointer approach works in linear time without any extra space.

1. Place one pointer `l` at the start and another `end` at the end of the array.
2. Compute the sum of `numbers[l]` and `numbers[end]`.
   - If the sum equals the target, return the indices (1-indexed).
   - If the sum is greater than the target, decrement `end` to reduce the sum.
   - If the sum is less than the target, increment `l` to increase the sum.
3. Repeat until the pair is found. Since exactly one solution is guaranteed, the loop always terminates with a match.

This works because the sorted order guarantees that moving the appropriate pointer is the only way to move toward the target sum without skipping a valid pair.

### Complexity

- **Time:** O(n) — each pointer moves at most n times total.
- **Space:** O(1) — only two index variables are used, satisfying the constant-space requirement.

## Solution

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, end = 0, len(numbers) - 1
        while l < end:
            current_sum = numbers[l] + numbers[end]
            if current_sum == target:
                return [l + 1, end + 1]
            elif current_sum > target:
                end -= 1
            else:
                l += 1

# Day 1 - Two Sum

**Link:** https://leetcode.com/problems/two-sum/
**Difficulty:** Easy
**Tags:** Array, Hash Table

## Problem
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers that add up to `target`. Each input has exactly one solution, and you may not use the same element twice.

## Approach
First pass: build a hash map storing each number's value as key and its index as value (`pos = {num: index}`).

Second pass: for each element, compute the complement (`target - nums[i]`). 
Check if this complement exists in the map and that its stored index isn't 
the same as the current index (to avoid using the same element twice). If 
found, return both indices.

## Complexity
- Time: O(n) — two linear passes through the array
- Space: O(n) — hash map storing up to n elements

## Notes
Used two separate passes instead of a single pass — slightly less optimal 
than the one-pass approach (since the map is fully built before checking), 
but still O(n) overall and easier to reason about.

## Code
\`\`\`python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        total_nums = len(nums)
        pos = {}
        for itr in range(total_nums):
            pos[nums[itr]] = itr

        for itr in range(total_nums):
            rem = target - nums[itr]
            if rem in pos and pos[rem] != itr:
                return [itr, pos[rem]]
\`\`\`

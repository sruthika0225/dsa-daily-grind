# Day 09 — Longest Common Prefix

**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** String · Prefix Matching · Iteration

---

## Problem Statement

Write a function to find the **longest common prefix** string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

---

### Example 1

**Input**

```text
strs = ["flower","flow","flight"]
```

**Output**

```text
"fl"
```

---

### Example 2

**Input**

```text
strs = ["dog","racecar","car"]
```

**Output**

```text
""
```

**Explanation**

There is no common prefix shared by all the strings.

---

## ✅ Approach — Prefix Reduction (Accepted)

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        pre = strs[0]

        for word in strs[1:]:
            while not word.startswith(pre):
                pre = pre[:-1]

                if pre == "":
                    return ""

        return pre
```

---

## Idea

Start by assuming that the **entire first string** is the common prefix.

Then compare this prefix with every other string:

- If the current string starts with the prefix, continue.
- Otherwise, remove the last character from the prefix.
- Repeat until the current string starts with the prefix.
- If the prefix becomes empty, there is no common prefix.

After checking every string, the remaining prefix is the answer.

---

## Dry Run

```text
strs = ["flower","flow","flight"]

Initial prefix = "flower"
```

### Compare with `"flow"`

```text
flower ❌
flowe  ❌
flow   ✅

Current prefix = "flow"
```

### Compare with `"flight"`

```text
flow ❌
flo  ❌
fl   ✅

Current prefix = "fl"
```

All strings processed.

Answer:

```text
"fl"
```

---

## Another Dry Run

```text
strs = ["dog","racecar","car"]

prefix = "dog"

dog ❌
do  ❌
d   ❌
""  ✅

Return ""
```

No common prefix exists.

---

## Why This Works

Every time the prefix fails to match a string, we shorten it by one character.

Since a common prefix cannot be longer than the shortest matching prefix found so far, repeatedly reducing it guarantees that:

- Any remaining prefix is common to all processed strings.
- The algorithm stops as soon as no common prefix exists.

---

## Complexity Analysis

Let:

- `n` = number of strings
- `m` = length of the shortest string

| Operation | Complexity |
|------------|------------|
| Prefix comparison | O(n × m) |
| Extra Space | O(1) |

In the worst case, each character of the prefix is removed at most once for each string.

---

## Constraints

- `1 ≤ strs.length ≤ 200`
- `0 ≤ strs[i].length ≤ 200`
- `strs[i]` consists only of lowercase English letters.

---

## Key Takeaway

Instead of comparing every character across all strings from the beginning, we can start with the **largest possible prefix** and gradually shrink it until it matches every string.

This approach is:

- Simple to implement
- Uses constant extra space
- Efficient for the given constraints

> **A common strategy in string problems is to begin with a candidate answer and repeatedly reduce it until it satisfies all conditions.**

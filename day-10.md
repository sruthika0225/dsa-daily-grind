# Day 10 — Valid Parentheses

**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** Stack · String

---

## Problem Statement

Given a string `s` containing only the characters `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`, determine whether the input string is valid.

A string is considered **valid** if:

- Every opening bracket has a corresponding closing bracket of the same type.
- Brackets are closed in the correct order.
- Every closing bracket has a matching opening bracket.

Return `true` if the string is valid; otherwise, return `false`.

---

### Example 1

**Input**

```text
s = "()"
```

**Output**

```text
true
```

---

### Example 2

**Input**

```text
s = "()[]{}"
```

**Output**

```text
true
```

---

### Example 3

**Input**

```text
s = "(]"
```

**Output**

```text
false
```

---

### Example 4

**Input**

```text
s = "([])"
```

**Output**

```text
true
```

---

### Example 5

**Input**

```text
s = "([)]"
```

**Output**

```text
false
```

---

## ✅ Approach — Stack (Accepted)

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []

        closing_brackets = {
            ")" : "(",
            "}" : "{",
            "]" : "["
        }

        for char in s:
            if closing_brackets.get(char):

                # No matching opening bracket
                if len(stack) == 0 or stack[-1] != closing_brackets[char]:
                    return False

                # Matching pair found
                stack.pop()

            else:
                stack.append(char)

        return len(stack) == 0
```

---

## Idea

A **stack** follows the **Last In, First Out (LIFO)** principle, making it perfect for matching parentheses.

Algorithm:

1. Traverse the string character by character.
2. If the character is an **opening bracket**, push it onto the stack.
3. If it is a **closing bracket**:
   - Check whether the stack is empty.
   - Verify that the top of the stack contains the corresponding opening bracket.
   - If not, return `False`.
   - Otherwise, pop the matching opening bracket.
4. After processing the entire string, the stack should be empty.

If the stack is empty, every bracket has been matched correctly.

---

## Dry Run

### Input

```text
s = "([])"
```

| Character | Stack | Action |
|-----------|-------|--------|
| ( | ( | Push |
| [ | ( [ | Push |
| ] | ( | Pop `[` |
| ) | Empty | Pop `(` |

Final Stack:

```text
[]
```

Return:

```text
True
```

---

### Another Dry Run

```text
s = "([)]"
```

| Character | Stack | Action |
|-----------|-------|--------|
| ( | ( | Push |
| [ | ( [ | Push |
| ) | ( [ | Expected `(` but found `[` → Invalid |

Return:

```text
False
```

---

## Why This Works

The most recently opened bracket must always be the first one to close.

For example:

```text
({[]})
```

Closing order:

```text
[]
{}
()
```

This exactly follows the **Last In, First Out (LIFO)** behavior of a stack.

Whenever a closing bracket appears, it must match the bracket at the top of the stack.

---

## Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Traversal | O(n) |
| Stack Operations | O(1) each |
| Overall Time | O(n) |
| Extra Space | O(n) |

where:

- `n = len(s)`

---

## Constraints

- `1 ≤ s.length ≤ 10⁴`
- `s` consists only of:

```text
'(' ')' '{' '}' '[' ']'
```

---

## Key Takeaway

Whenever a problem involves **matching pairs**, **nested structures**, or checking the **most recent unmatched element**, a **stack** is often the ideal data structure.

In this problem:

- Opening brackets are pushed onto the stack.
- Closing brackets must match the most recently opened bracket.
- Any mismatch or leftover brackets indicate an invalid string.

This results in an efficient solution with:

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

> **Stacks are the go-to data structure for problems involving balanced symbols, nested expressions, and undo-like operations.**

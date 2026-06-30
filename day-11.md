# Day 11 — Add Binary

**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** String · Bit Manipulation · Simulation

---

## Problem Statement

Given two binary strings `a` and `b`, return their sum as a binary string.

The input strings consist only of `'0'` and `'1'` characters and represent valid binary numbers.

---

### Example 1

**Input**

```text
a = "11"
b = "1"
```

**Output**

```text
"100"
```

---

### Example 2

**Input**

```text
a = "1010"
b = "1011"
```

**Output**

```text
"10101"
```

---

## ✅ Approach — Simulate Binary Addition (Accepted)

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        carry = 0
        lena = len(a)
        lenb = len(b)
        index = -1
        res = ""

        while (lena + index) >= 0 or (lenb + index) >= 0:
            lasta = int(a[index]) if (lena + index) >= 0 else 0
            lastb = int(b[index]) if (lenb + index) >= 0 else 0

            if carry + lasta + lastb == 0:
                carry = 0
                res = "0" + res

            elif carry + lasta + lastb == 1:
                carry = 0
                res = "1" + res

            elif carry + lasta + lastb == 2:
                carry = 1
                res = "0" + res

            elif carry + lasta + lastb == 3:
                carry = 1
                res = "1" + res

            index -= 1

        return str(carry) + res if carry > 0 else res
```

---

## Idea

This problem is similar to the way we perform **addition by hand**, except we're working in **binary (base 2)**.

Algorithm:

1. Start from the last character of both strings.
2. Add:
   - Current bit from `a`
   - Current bit from `b`
   - Current `carry`
3. Determine:
   - The resulting binary digit.
   - The new carry.
4. Repeat until both strings have been completely processed.
5. If a carry remains at the end, add it to the front of the result.

---

## Dry Run

### Input

```text
a = "1010"
b = "1011"
```

Process from right to left.

| a | b | Carry In | Sum | Result Bit | Carry Out |
|---|---|----------|-----|------------|-----------|
|0|1|0|1|1|0|
|1|1|0|2|0|1|
|0|0|1|1|1|0|
|1|1|0|2|0|1|

Carry remains:

```text
1
```

Final answer:

```text
10101
```

---

## Why This Works

Binary addition has only four possible cases.

| Sum | Result Bit | Carry |
|-----|------------|--------|
|0|0|0|
|1|1|0|
|2|0|1|
|3|1|1|

For every position, we simply calculate:

```text
carry + bit_from_a + bit_from_b
```

Based on this value, we determine the current result bit and the carry for the next iteration.

---

## Complexity Analysis

Let:

- `n = len(a)`
- `m = len(b)`

| Operation | Complexity |
|-----------|------------|
| Traversal | O(max(n, m)) |
| Extra Space | O(max(n, m)) |

The algorithm visits each bit exactly once.

---

## Constraints

- `1 ≤ a.length, b.length ≤ 10⁴`
- `a` and `b` contain only `'0'` and `'1'`.
- Neither string has leading zeros except the number `"0"`.

---

## Key Takeaway

Instead of converting the binary strings into integers, we can simulate the addition directly.

This approach:

- Works efficiently even for very large binary numbers.
- Avoids integer overflow in languages with fixed-size integer types.
- Mimics elementary binary addition using a carry.

This results in:

- **Time Complexity:** O(max(n, m))
- **Space Complexity:** O(max(n, m))

> **Many string arithmetic problems can be solved by simulating manual addition from right to left while maintaining a carry.**

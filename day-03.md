# Mini-Max Sum

> **HackerRank** · Warm-Up Challenge · [Problem Link](https://www.hackerrank.com/challenges/mini-max-sum/problem)

---

## Problem Statement

Given five positive integers, find the **minimum** and **maximum** values that can be calculated by summing exactly **four of the five** integers. Print the respective minimum and maximum values as a single line of two space-separated long integers.

---

## Examples

### Example 1
**Input:**
```
1 2 3 4 5
```
**Output:**
```
10 14
```
**Explanation:**
- All possible 4-element sums: 2+3+4+5=14, 1+3+4+5=13, 1+2+4+5=12, 1+2+3+5=11, 1+2+3+4=10
- Minimum = **10**, Maximum = **14**

---

## Approach

Instead of generating all possible 4-element subsets, we use a simple mathematical observation:

| Goal | Action |
|------|--------|
| **Minimum sum** | Sum all 5 elements, then **subtract the maximum** element |
| **Maximum sum** | Sum all 5 elements, then **subtract the minimum** element |

This works because leaving out the **largest** element gives the smallest possible sum, and leaving out the **smallest** element gives the largest possible sum.

```
total   = sum(arr)
minimum = total - max(arr)
maximum = total - min(arr)
```

---

## Complexity

| | Complexity |
|---|---|
| **Time** | O(n) |
| **Space** | O(1) |

---

## Solution

```python
#!/bin/python3

def miniMaxSum(arr):
    total = sum(arr)
    minimum = total - max(arr)
    maximum = total - min(arr)
    print(f"{minimum} {maximum}")

if __name__ == '__main__':
    arr = list(map(int, input().rstrip().split()))
    miniMaxSum(arr)
```

---

## Constraints

- Each integer in the array: 1 ≤ value ≤ 10⁹
- Array always contains exactly **5** integers
- Use `long` / 64-bit integers in C/C++/Java to avoid overflow

---

## How to Run

```bash
# Clone the repo
git clone https://github.com/<your-username>/hackerrank-solutions.git
cd hackerrank-solutions/warm-up/mini-max-sum

# Run with sample input
echo "1 2 3 4 5" | python3 mini_max_sum.py
# Output: 10 14
```

---

## Tags

`#hackerrank` `#python` `#warm-up` `#arrays` `#math`

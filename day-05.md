# Day 05 — Best Time to Buy and Sell Stock

**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** Arrays · Greedy · Dynamic Programming

---

## Problem Statement

You are given an array `prices` where `prices[i]` represents the price of a stock on the `iᵗʰ` day.

You want to maximize your profit by choosing **one day to buy** and a **different day in the future to sell**.

Return the maximum profit you can achieve. If no profit is possible, return `0`.

### Example 1

**Input**

```text
prices = [7,1,5,3,6,4]
```

**Output**

```text
5
```

**Explanation**

Buy on day 2 at price `1` and sell on day 5 at price `6`.

Profit = `6 - 1 = 5`

---

### Example 2

**Input**

```text
prices = [7,6,4,3,1]
```

**Output**

```text
0
```

**Explanation**

Prices keep decreasing, so no profitable transaction exists.

---

## Approaches

---

## ❌ Approach 1 — Brute Force (TLE)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        total = len(prices)
        max_profit = 0

        for itr in range(total):
            for jtr in range(itr + 1, total):
                profit = prices[jtr] - prices[itr]

                if profit > max_profit:
                    max_profit = profit

        return max_profit
```

### Idea

Try every possible pair:

- Buy on day `i`
- Sell on every future day `j`
- Calculate the profit
- Keep track of the maximum profit found

---

### Why it TLEs

The nested loops compare every pair of days.

| Operation | Cost |
|------------|------|
| Outer loop | O(n) |
| Inner loop | O(n) |
| Total | O(n²) |

For `n = 10⁵`:

```text
10⁵ × 10⁵ = 10¹⁰ operations
```

That's billions of comparisons, causing **Time Limit Exceeded (TLE)**.

---

## ✅ Approach 2 — Track Minimum Price (Accepted)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = float('inf')
        max_profit = 0

        for price in prices:
            if price < min_price:
                min_price = price
            elif price - min_price > max_profit:
                max_profit = price - min_price

        return max_profit
```

### Idea

Instead of checking every pair:

1. Keep track of the **lowest price seen so far**.
2. For each current price:
   - Assume we sell today.
   - Profit = `current_price - minimum_price_seen`.
3. Update the maximum profit whenever a better profit is found.

---

### Dry Run

```text
prices = [7,1,5,3,6,4]

Price   Min Price   Profit   Max Profit
7          7          0          0
1          1          0          0
5          1          4          4
3          1          2          4
6          1          5          5
4          1          3          5
```

Answer = **5**

---

## Complexity Analysis

| Approach | Time | Space |
|-----------|------|--------|
| Brute Force | O(n²) | O(1) |
| Minimum Price Tracking | O(n) | O(1) |

---

## Constraints

- `1 ≤ prices.length ≤ 10⁵`
- `0 ≤ prices[i] ≤ 10⁴`

---

## Key Takeaway

The brute-force approach checks every possible buy-sell combination, leading to **O(n²)** time complexity and TLE.

By keeping track of the **minimum price encountered so far**, we can determine the best profit at each day in a single pass, reducing the complexity to **O(n)**.

**Sometimes, instead of comparing every pair, maintaining the right information while traversing once is enough.**

# Day 06 — Merge Two Sorted Lists

**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** Linked Lists · Recursion · Two Pointers


---

## Problem Statement

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

---

### Example 1

**Input**

```text
list1 = [1,2,4]
list2 = [1,3,4]
```

**Output**

```text
[1,1,2,3,4,4]
```

---

### Example 2

**Input**

```text
list1 = []
list2 = []
```

**Output**

```text
[]
```

---

### Example 3

**Input**

```text
list1 = []
list2 = [0]
```

**Output**

```text
[0]
```

---

## Approach — Iterative Merge (Accepted)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeTwoLists(
        self,
        list1: Optional[ListNode],
        list2: Optional[ListNode]
    ) -> Optional[ListNode]:

        result = ListNode(0)
        current = result

        while list1 and list2:
            if list1.val < list2.val:
                current.next = list1
                list1 = list1.next
            else:
                current.next = list2
                list2 = list2.next

            current = current.next

        if list1:
            current.next = list1
        elif list2:
            current.next = list2

        return result.next
```

---

## Idea

Since both linked lists are already sorted, we can merge them similarly to the merge step of Merge Sort.

1. Create a **dummy node** to simplify handling the head of the merged list.
2. Maintain a pointer `current` to the last node in the merged list.
3. Compare the current nodes of both lists:
   - Attach the smaller node to `current.next`.
   - Move the corresponding list pointer forward.
4. Advance `current`.
5. Once one list becomes empty, append the remaining nodes of the other list.

Finally, return `result.next` because `result` is just the dummy node.

---

## Dry Run

```text
list1 = [1,2,4]
list2 = [1,3,4]

Compare 1 and 1
→ Take 1 from list2

Merged: 1

Compare 1 and 3
→ Take 1 from list1

Merged: 1 → 1

Compare 2 and 3
→ Take 2 from list1

Merged: 1 → 1 → 2

Compare 4 and 3
→ Take 3 from list2

Merged: 1 → 1 → 2 → 3

Compare 4 and 4
→ Take 4 from list2

Merged: 1 → 1 → 2 → 3 → 4

list2 exhausted

Append remaining nodes from list1

Final List:
1 → 1 → 2 → 3 → 4 → 4
```

---

## Why Use a Dummy Node?

Without a dummy node, special care is needed when inserting the first element because the head of the merged list is not known initially.

Using:

```python
result = ListNode(0)
```

allows us to build the merged list uniformly and simply return:

```python
result.next
```

---

## Complexity Analysis

| Operation | Complexity |
|------------|------------|
| Traversing both lists | O(n + m) |
| Extra space | O(1) |

where:

- `n` = length of `list1`
- `m` = length of `list2`

---

## Constraints

- The number of nodes in both lists is in the range `[0, 50]`
- `-100 ≤ Node.val ≤ 100`
- Both lists are sorted in non-decreasing order

---

## Key Takeaway

Since both lists are already sorted, there's no need to copy values into an array and sort again.

By maintaining pointers to both lists and always choosing the smaller node, we can merge them efficiently in **O(n + m)** time with **constant extra space**.

This problem introduces an important Linked List technique:

> **Using a dummy node to simplify pointer manipulation and avoid edge cases.**

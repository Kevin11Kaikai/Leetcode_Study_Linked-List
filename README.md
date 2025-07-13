# 📘 Leetcode Study: Linked List - Problem 203

## 🚀 Problem: Remove Linked List Elements

Remove all elements from a linked list of integers that have a specific value.

---

## 📌 Table of Contents

- [Introduction](#introduction)
- [Python Solution](#python-solution)
- [Concept Summary](#concept-summary)
- [Key Knowledge Points](#key-knowledge-points)
- [Deletion Approach](#deletion-approach)
- [Step-by-Step Example](#step-by-step-example)
- [Common Mistakes](#common-mistakes)
- [Takeaways](#takeaways)
- [Complexity Analysis](#complexity-analysis)

---

## 🧠 Introduction

A **Linked List** is a linear data structure where each element (node) contains:
- A value (`.val`)
- A pointer to the next node (`.next`)

It differs from arrays in that it uses **non-contiguous memory**, offering constant-time insertions/deletions but linear-time access.

---

## ✅ Python Solution (with Comments)

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        # Create a dummy node to simplify edge case deletions
        dummy = ListNode(-1)
        dummy.next = head
        current = dummy

        while current.next:
            if current.next.val == val:
                current.next = current.next.next  # Skip target node
            else:
                current = current.next

        return dummy.next
```

---

## 🧩 Concept Summary

| Feature             | Array                | Linked List             |
|---------------------|----------------------|--------------------------|
| Memory Layout       | Contiguous           | Non-contiguous (pointers) |
| Random Access       | O(1)                 | O(n)                    |
| Insertion/Deletion  | O(n) (shift needed)  | O(1) (adjust `.next`)   |
| Data Return         | Full array           | Starting node (`head`)  |

---

## 📚 Key Knowledge Points

### 1. ListNode Usage

```python
a = ListNode(1)
b = ListNode(2)
a.next = b  # a → b
```

- Lists are manually constructed, node-by-node.

### 2. Dummy Node Trick

To safely remove the head or manage edge cases:

```python
dummy = ListNode(-1)
dummy.next = head
```

This allows uniform deletion logic and avoids special-case handling.

---

## 🔧 Deletion Approach

**Goal:** Remove all nodes where `node.val == val`

**Strategy:**

1. Create a dummy node pointing to `head`
2. Use `current = dummy` to start traversal
3. If `current.next.val == val`, skip the node
4. Return `dummy.next` as the new head

---

## 📝 Step-by-Step Example

Given:
```python
head = [6, 2, 6, 3, 4, 5, 6]
val = 6
```

**Execution:**

```
Initial: dummy → 6 → 2 → 6 → 3 → 4 → 5 → 6
Remove 6: dummy → 2 → 6 → 3 → 4 → 5 → 6
Remove 6: dummy → 2 → 3 → 4 → 5 → 6
Remove 6: dummy → 2 → 3 → 4 → 5
Return:   dummy.next → 2 → 3 → 4 → 5
```

---

## ⚠️ Common Mistakes

| Mistake | Why it Fails |
|--------|---------------|
| `return head` | ❌ If `head` is deleted, it points to an invalid node. |
| `current = head` | ❌ You can't delete `head` without accessing its previous node. |
| `if current.val == val:` | ❌ You need to check `current.next.val` to delete correctly. |

---

## ✅ Takeaways

- Use a **dummy node** to handle edge cases, especially head deletion.
- Always **check `current.next`**, not `current` itself.
- Always **return `dummy.next`**, not `head`.
- Linked lists are chains of references, **not** memory blocks.

---

## ⏰ Complexity Analysis

| Metric            | Value     |
|-------------------|-----------|
| Time Complexity   | O(n)      |
| Space Complexity  | O(1)      |

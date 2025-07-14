# 📘 Leetcode Study: Linked List 

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


# 🚀 Leetcode 206 - Reverse Linked List

---

## ✅ Python Code (with Full Comments)

```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None                  # Previous node (tail of reversed list)
        current = head               # Current node in original list

        while current:
            next_node = current.next  # 🔁 Save next node before cutting
            current.next = prev       # 🔁 Reverse the pointer
            prev = current            # Move prev forward (new head grows)
            current = next_node       # Move current forward (continue traversal)

        return prev  # New head of reversed list
```

---

## ⏱️ Complexity

| Metric           | Value |
|------------------|--------|
| Time Complexity  | O(n)   |
| Space Complexity | O(1)   |

---

## 🧠 Intuition & Visualization

### Original List:
```
head → 1 → 2 → 3 → 4 → 5 → None
```

### Reversed:
```
5 → 4 → 3 → 2 → 1 → None
```

---

### 🔁 Step-by-Step Example: [1 → 2 → 3]

Initial:
```
prev    = None
current = 1 → 2 → 3
```

Step 1:
```
next_node = 2
current.next = prev → 1 → None
prev = 1
current = 2
```

Step 2:
```
next_node = 3
current.next = prev → 2 → 1 → None
prev = 2
current = 3
```

Step 3:
```
next_node = None
current.next = prev → 3 → 2 → 1 → None
prev = 3
current = None (done)
```

---

## 🧭 Why Use Two Pointers (`prev` and `current`)?

| Pointer | Purpose                             |
|---------|-------------------------------------|
| `current` | Traverses the original list         |
| `prev`    | Rebuilds the reversed list from tail |

- You **must** preserve `current.next` before reversing the link, or you'll lose access to the rest of the list.
- One pointer is not enough — reversing is a **destructive operation**, so you need to **save and rebuild simultaneously**.

---

## 🔄 Mental Analogy

> Imagine walking across a rope bridge. Every step you take, you must detach the plank behind and re-attach it in reverse.  
> You need one hand to hold the old bridge (`current`) and one hand to rebuild the reversed one (`prev`).

---

## ⚠️ Mistake Log: What I Tried and Why It Failed

### ❌ Mistake 1: Forgetting to save `next_node`

```python
current.next = prev
current = current.next  # 💥 current now points to prev, not the next node
```

**Bug:**
You overwrote the `.next` pointer before saving it. Now you've lost the rest of the list.

---

### ❌ Mistake 2: Wrong update order

```python
prev = current
current.next = prev  # 💥 creates a cycle!
```

**Bug:**
This makes a loop: node points to itself. Always reverse pointer first, then move `prev` forward.

---

### ❌ Mistake 3: Only using one pointer

Trying to do everything with just `current` is impossible:
- You’ll lose the original path once you reverse the link.
- No way to “re-enter” the list unless you stored the `next_node`.

---

## ✅ Key Takeaways

- ✅ Use two pointers: `current` walks the list; `prev` builds the reversed one.
- ✅ Always save `next_node` before reversing.
- ✅ Reversing is a **destructive** operation — without saving, you lose the rest.
- ✅ Final result is `prev`, not `head`, because `head` becomes the tail.

---

## 📌 Summary

> Reversing a linked list is **not just pointer flipping** — it’s a process of **simultaneous teardown and reconstruction**.

Use the pattern:

```text
Save → Flip → Advance → Repeat
```


# Leetcode_Study_Linked List
## 🚀 LeetCode 203 - Remove Linked List Elements (Deep Dive Version)

---

## ✅ Python Code (with Explanatory Comments)

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val        # value stored in the node
        self.next = next      # pointer to the next node           

class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        # Step 1: Create a dummy node before head to simplify edge cases
        dummy = ListNode(-1)
        dummy.next = head     # dummy links to the head

        # Step 2: Start traversal from dummy (not head!)
        current = dummy

        # Step 3: Use current.next to check and remove target nodes
        while current.next:
            if current.next.val == val:
                current.next = current.next.next  # skip the target node
            else:
                current = current.next            # move forward

        # Step 4: Return the new head (could be different from original head)
        return dummy.next
```
✅ Linked List — Core Concepts & Common Pitfalls

🧩 Concept Summary

A Linked List is a linear data structure where each element (called a node) contains:

A value (.val)

A pointer to the next node (.next)

Unlike arrays, linked lists do not store elements in contiguous memory blocks. This makes certain operations easier (like insertion/deletion), but sacrifices constant-time random access.

📚 Key Knowledge Points

1. Memory Layout

Concept

Array

Linked List

Memory layout

Contiguous

Non-contiguous, pointer-based

Random access

O(1) via arr[i]

O(n) — must traverse from head

Insertion/deletion

O(n) — shift elements

O(1) — adjust .next pointers

Return data

Full array

Only return the starting node head

2. Basic ListNode Usage

a = ListNode(1)
b = ListNode(2)
a.next = b  # a → b

Each node links explicitly to the next.

Lists are built manually — no implicit structure like arrays.

3. Dummy Node Trick

You can't delete the head node directly using current.next because there's no node before head.

Solution: Create a dummy node:

dummy = ListNode(-1)
dummy.next = head

Now you can safely delete head if needed, and always maintain a reference to the previous node.

🧠 Approach: Deletion in Linked List

Problem:

Remove all nodes with a given val.

Core Strategy:

Use a dummy node to simplify head deletion.

Use current to iterate, always checking current.next.

If current.next.val == val, remove it by skipping.

📝 Step-by-Step Example

head = [6, 2, 6, 3, 4, 5, 6]
val = 6

Execution:

Step 0: dummy → 6 → 2 → 6 → 3 → 4 → 5 → 6
Step 1: remove 6      → dummy → 2 → 6 → 3 → 4 → 5 → 6
Step 2: remove 6      → dummy → 2 → 3 → 4 → 5 → 6
Step 3: remove 6      → dummy → 2 → 3 → 4 → 5
Return dummy.next     → 2 → 3 → 4 → 5

✅ Python Code with Comments

class Solution:
    def removeElements(self, head, val):
        dummy = ListNode(-1)
        dummy.next = head
        current = dummy

        while current and current.next:
            if current.next.val == val:
                current.next = current.next.next
            else:
                current = current.next

        return dummy.next

⚠️ Mistake Log: Common Errors and Why They Fail

❌ Mistake 1: Returning head

return head

Bug: If head is deleted, this points to a removed node. Always return dummy.next.

❌ Mistake 2: Starting from head, not dummy

current = head

Bug: You can’t delete head without knowing the previous node. Dummy helps fix this.

❌ Mistake 3: Checking current instead of current.next

if current.val == val:
    current = current.next

Bug: This skips checking the node that needs deletion. Deletion requires:

current.next = current.next.next

✅ Key Takeaways

✅ Use a dummy node to uniformly delete any node — including head.

✅ Always check and update current.next instead of current.

✅ Always return dummy.next, not head, to get the updated list.

✅ Linked lists are chains of node references, not blocks like arrays.

⏰ Complexity

Metric

Value

Time Complexity

O(n)

Space Complexity

O(1)



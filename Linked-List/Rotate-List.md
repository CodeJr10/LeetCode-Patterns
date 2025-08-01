# 🔁 Rotate Linked List to the Right

## 📘 Problem Description

Given the head of a singly linked list, rotate the list to the right by `k` places.

The rotation means that each node is shifted right by one position, and the last node moves to the front. This process is repeated `k` times.

---

## 🔐 Constraints

- The number of nodes in the list is in the range `[0, 500]`.
- `0 <= k <= 2 * 10⁹`
- `-100 <= Node.val <= 100`

---

## 🧾 Java Code

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null || k == 0) return head;

        ListNode tail = head;
        int len = 1;

        // Find the length and the last node
        while (tail.next != null) {
            len++;
            tail = tail.next;
        }

        k = k % len;
        if (k == 0) return head;

        // Make it circular
        tail.next = head;

        // Find new tail (len - k)th node
        ListNode newTail = findNthNode(head, len - k);

        // Break the circle
        head = newTail.next;
        newTail.next = null;

        return head;
    }

    private ListNode findNthNode(ListNode temp, int k) {
        int count = 1;
        while (temp != null) {
            if (count == k) return temp;
            count++;
            temp = temp.next;
        }
        return temp;
    }
}
```
---

## 📈 Time and Space Complexity
Time Complexity: O(N)

Space Complexity: O(1)


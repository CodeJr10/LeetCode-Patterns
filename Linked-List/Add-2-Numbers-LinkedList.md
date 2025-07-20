# 🧮 Add Two Numbers in Linked List (Reverse Order)

## 📘 Problem Description

Given two non-empty linked lists `l1` and `l2` representing two non-negative integers,  
**where digits are stored in reverse order**, and each of their nodes contains a single digit,  
add the two numbers and return the **sum as a linked list**, also in reverse order.

✅ You may assume the two numbers **do not contain any leading zero**, except the number 0 itself.

---

## 🧠 Examples

### Example 1

**Input**:
l1 = 5 -> 4
l2 = 4

**Explanation**:
l1 = 45 (reversed list)
l2 = 4
Sum = 49
Output = 9 -> 4

---

### Example 2

**Input**:
l1 = 4 -> 5 -> 6
l2 = 1 -> 2 -> 3

**Explanation**:
l1 = 654, l2 = 321
Sum = 975
Output = 5 -> 7 -> 9

---

## 🔐 Constraints

- 1 ≤ number of nodes in each linked list ≤ 100
- 0 ≤ Node.val ≤ 9
- Input lists represent a non-negative integer in reverse order
- There are no leading zeros unless the number is zero

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0); // dummy node to build result
        ListNode curr = dummy;
        int carry = 0;

        while (l1 != null || l2 != null || carry != 0) {
            int val1 = (l1 != null) ? l1.val : 0;
            int val2 = (l2 != null) ? l2.val : 0;

            int sum = val1 + val2 + carry;
            carry = sum / 10;

            curr.next = new ListNode(sum % 10);
            curr = curr.next;

            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }

        return dummy.next;
    }
}

```
## 🧪 Dry Run

l1 = 2 -> 4 -> 3  (represents 342)
l2 = 5 -> 6 -> 4  (represents 465)

Step-by-step:
2 + 5 = 7          -> result: 7
4 + 6 = 10         -> result: 0, carry: 1
3 + 4 + 1 = 8      -> result: 8

#### Output: 7 -> 0 -> 8 (represents 807)
---
## 📈 Time and Space Complexity
#### Time Complexity: O(max(n, m))
(where n and m are the lengths of the two input linked lists)

#### Space Complexity: O(max(n, m))
(for the result list and carry handling)

🙌 Tips
Use a dummy node to simplify edge cases.

Always check for carry in each iteration.

Handle different lengths of input lists gracefully.

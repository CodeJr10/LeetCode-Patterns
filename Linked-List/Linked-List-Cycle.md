📘 Detect Cycle in a Linked List
Problem:
Given head, the head of a linked list, determine if the linked list has a cycle in it.
A linked list has a cycle if there is some node in the list that can be reached again by continuously following the next pointer.

Return true if there is a cycle in the linked list. Otherwise, return false.

🧠 Approach
This uses Floyd’s Cycle Detection Algorithm (also known as the Tortoise and Hare Algorithm):

Initialize two pointers:

slow → moves one step at a time

fast → moves two steps at a time

If there is a cycle, slow and fast will eventually meet at some point.

If fast or fast.next becomes null, then the list has no cycle.

✅ Example
Input:
bash
Copy
Edit
head = [3,2,0,-4], pos = 1 (tail connects to node index 1)
Output:
arduino
Copy
Edit
true
Explanation:
There is a cycle because the tail node -4 connects to node 2.

🧾 Code
java
Copy
Edit
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            
            if(slow == fast){
                return true;
            }
        }
        return false;
    }
}
🧩 Time & Space Complexity
Time Complexity: O(n) — At most, all nodes are visited once by both pointers.

Space Complexity: O(1) — Constant space usage.

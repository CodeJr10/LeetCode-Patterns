
# 🧮 MinStack Implementation

## ✅ Problem Statement

Design a stack that supports **push**, **pop**, **top**, and retrieving the **minimum element** in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element.
- `int getMin()` retrieves the minimum element in the stack.

All operations must be performed in **O(1)** time complexity.

---

## 💡 Approach

To maintain a **running minimum** at each level of the stack, we use a custom **linked list node** structure. Each node stores:
- Its value `val`
- The minimum `min` **at the time it was pushed**
- A pointer to the next node (`next`)

The `head` of the list acts as the **top of the stack**.

By doing this, each operation:
- `push` simply compares and stores the current minimum with the previous one.
- `getMin` returns the minimum stored at the head.
- `top` returns the value at the head.
- `pop` updates the head pointer.

No additional stack is required!

---

## 🧠 Key Concepts

- **Encapsulation**: The `Node` class is private and hidden from users of `MinStack`, enforcing abstraction.
- **Time Complexity**:
  - `push`: O(1)
  - `pop`: O(1)
  - `top`: O(1)
  - `getMin`: O(1)
- **Space Complexity**: O(N), where N is the number of elements pushed.

---

## ✅ Java Code

```java
class MinStack {
    private Node head;

    public void push(int x) {
        if (head == null)
            head = new Node(x, x, null);
        else
            head = new Node(x, Math.min(x, head.min), head);
    }

    public void pop() {
        head = head.next;
    }

    public int top() {
        return head.val;
    }

    public int getMin() {
        return head.min;
    }

    // Private inner class Node
    private class Node {
        int val;
        int min;
        Node next;

        private Node(int val, int min, Node next) {
            this.val = val;
            this.min = min;
            this.next = next;
        }
    }
}
```

## 🔍 Example

MinStack st = new MinStack();
st.push(5);
st.push(2);
st.push(3);
st.getMin(); // returns 2
st.pop();
st.getMin(); // still returns 2
st.pop();
st.getMin(); // returns 5
Each node keeps track of the min value at that point, making getMin() an O(1) operation.

## 🎯 Summary
This approach leverages a custom singly-linked list to simulate stack behavior while tracking minimums. It’s efficient, clean, and avoids the need for extra data structures.

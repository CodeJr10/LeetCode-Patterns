# 🔁 Next Greater Element II (Leetcode 503)

## 🧠 Problem Statement

Given a **circular integer array** `nums`, return the **Next Greater Number** for every element.  
The Next Greater Number of a number `x` is the **first greater number to its traversing-order next in the array**,  
which means you loop back to the beginning if needed.

If it doesn’t exist, return -1 for this number.

---

## 💡 Example:

### Input:
nums = [2, 10, 12, 1, 11]

### Output:
[10, 12, -1, 11, 12]


### Explanation:
- Next greater for `2` → `10`
- Next greater for `10` → `12`
- Next greater for `12` → no greater → `-1`
- Next greater for `1` → `11`
- Next greater for `11` → `12` (because it's circular)

---

## 📦 Intuition:

To simulate a **circular array**, we iterate from `2n - 1` to `0` and access elements using `i % n`.

We maintain a **monotonic stack** (decreasing order) to keep track of next greater elements efficiently.

---

## 🚀 Approach:

1. Traverse the array **from right to left**, from `i = 2n - 1` to `0`.
2. Use `i % n` to wrap around the array.
3. Use a **stack** to store candidates for the next greater element.
4. Pop from stack until the top is **greater** than the current element.
5. If stack is empty → `-1` is the answer.
6. Push the current element into the stack.

---

## 💻 Code (Java)

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int[] nge = new int[n];
        Stack<Integer> st = new Stack<>();

        for (int i = 2 * n - 1; i >= 0; i--) {
            int curr = nums[i % n];

            while (!st.isEmpty() && st.peek() <= curr) {
                st.pop();
            }

            if (i < n) {
                nge[i] = st.isEmpty() ? -1 : st.peek();
            }

            st.push(curr);
        }

        return nge;
    }
}

```
---
## ⏱️ Time & Space Complexity
#### Time: O(2N) → We loop twice over the array (for circularity).

#### Space: O(N) → For the monotonic stack.

🧪 Test it:

int[] nums = {2, 10, 12, 1, 11};
// Output: [10, 12, -1, 11, 12]

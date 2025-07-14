# 🔙 Previous Smaller Element (Monotonic Stack)

## 🧩 Problem Statement

Given an array of integers, for each element, find the **Previous Smaller Element (PSE)** — the closest element to the left that is **smaller** than the current element. If there is no such element, return -1 for that position.

### 🧪 Example

Input:
arr = [4, 5, 2, 10, 8]

Output:
[-1, 4, -1, 2, 2]

### 💡 Explanation

- `4` → no smaller on left → `-1`
- `5` → `4` is smaller → `4`
- `2` → nothing smaller before it → `-1`
- `10` → `2` is the previous smaller → `2`
- `8` → `2` is smaller and closer than `10` → `2`

---

## 🚀 Intuition

We need to **find the closest smaller element on the left** for each number. A brute-force approach would be O(n²), but we can do it in O(n) using a **monotonic increasing stack**.

The stack will store **possible candidates** for previous smaller elements.

---

## 🔂 Dry Run

Let’s say `arr = [4, 5, 2, 10, 8]`

| Index | Element | Stack           | Answer |
|-------|---------|------------------|--------|
| 0     | 4       | [4]              | -1     |
| 1     | 5       | [4, 5]           | 4      |
| 2     | 2       | [2]              | -1     |
| 3     | 10      | [2, 10]          | 2      |
| 4     | 8       | [2, 8]           | 2      |

---

## 🧠 Approach

1. Initialize an empty stack and a result list.
2. Loop through each element:
   - While the stack is **not empty** and the top of the stack is **greater than or equal to** the current element, **pop** the stack.
   - If the stack is empty → no smaller element → append `-1`.
   - Else → the top of the stack is the previous smaller element → append it.
   - Push current element to stack.
3. Return the result array.

---

## 📦 Time & Space Complexity

- **Time Complexity:** O(n) — each element is pushed and popped at most once
- **Space Complexity:** O(n) — for the stack and output array

---

## 📜 Java Code

```java
import java.util.*;

public class PreviousSmallerElement {
    public static int[] previousSmaller(int[] arr) {
        int n = arr.length;
        int[] res = new int[n];
        Stack<Integer> st = new Stack<>();

        for (int i = 0; i < n; i++) {
            while (!st.isEmpty() && st.peek() >= arr[i]) {
                st.pop();
            }

            res[i] = st.isEmpty() ? -1 : st.peek();
            st.push(arr[i]);
        }

        return res;
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {4, 5, 2, 10, 8};
        System.out.println("Input: " + Arrays.toString(arr));
        System.out.println("Previous Smaller Elements: " + Arrays.toString(previousSmaller(arr)));
    }
}
```
## 🏁 Output

Input: [4, 5, 2, 10, 8]
Previous Smaller Elements: [-1, 4, -1, 2, 2]

# 🧮 Sum of Subarray Minimums (Leetcode 907)

## 🔒 Problem Statement

Given an array of integers `arr`, find the **sum of the minimum** of every (contiguous) subarray of `arr`.

Since the answer may be large, **return the answer modulo 10⁹ + 7**.

---

## 🧾 Example 1

**Input:**
arr = [3,1,2,4]

**Output:**
17

**Explanation:**
All subarrays and their minimums:

- [3] → 3  
- [1] → 1  
- [2] → 2  
- [4] → 4  
- [3,1] → 1  
- [1,2] → 1  
- [2,4] → 2  
- [3,1,2] → 1  
- [1,2,4] → 1  
- [3,1,2,4] → 1

Sum = 3 + 1 + 2 + 4 + 1 + 1 + 2 + 1 + 1 + 1 = **17**

---

## 🧾 Example 2

**Input:**
arr = [11,81,94,43,3]

**Output:**
444
---

## 💡 Approach

We need to find, for each element `arr[i]`, how many subarrays it appears in as the **minimum**.

To do this, we calculate:
- **Previous Less Element (PLE):** index of the first element to the left that is strictly less than `arr[i]`
- **Next Less Element (NLE):** index of the first element to the right that is **less than or equal to** `arr[i]`

Then, total subarrays in which `arr[i]` is the minimum = `(i - ple[i]) * (nle[i] - i)`

Multiply this count with `arr[i]` and add to the result.

We use **monotonic stacks** to find PLE and NLE efficiently in O(N) time.

---

## ✅ Java Code

```java
import java.util.*;

public class Solution {
    public int sumSubarrayMins(int[] arr) {
        int n = arr.length;
        int mod = (int)1e9 + 7;

        Stack<Integer> stack = new Stack<>();
        int[] ple = new int[n];
        int[] nle = new int[n];

        // Previous Less Element
        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && arr[stack.peek()] > arr[i]) {
                stack.pop();
            }
            ple[i] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(i);
        }

        stack.clear();

        // Next Less Element
        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) {
                stack.pop();
            }
            nle[i] = stack.isEmpty() ? n : stack.peek();
            stack.push(i);
        }

        long sum = 0;
        for (int i = 0; i < n; i++) {
            long left = i - ple[i];
            long right = nle[i] - i;
            sum = (sum + arr[i] * left * right) % mod;
        }

        return (int)sum;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.sumSubarrayMins(new int[]{3, 1, 2, 4})); // Output: 17
        System.out.println(sol.sumSubarrayMins(new int[]{11, 81, 94, 43, 3})); // Output: 444
    }
}

```
---
## 🧠 Time & Space Complexity
#### Time Complexity: O(n)

#### Space Complexity: O(n) — for PLE, NLE, and stack


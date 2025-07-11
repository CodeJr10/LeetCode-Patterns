# 🔢 496. Next Greater Element I

## 🧩 Problem Statement

The **next greater element** of some element `x` in an array is the **first greater element to the right of `x`** in the same array.

You are given two **distinct** 0-indexed integer arrays `nums1` and `nums2`, where `nums1` is a **subset** of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the **next greater element** of `nums2[j]` in `nums2`. If there is no next greater element, then the answer is **-1**.

Return an array `ans` of length `nums1.length` such that `ans[i]` is the next greater element as described above.

---

## 🚀 Approach

We will use a **Monotonic Stack** and a **HashMap**:

1. **Traverse** `nums2` from **left to right**
2. Maintain a **decreasing stack** (top of the stack is always the greater element)
3. If the current number is **greater than the top**, pop the stack and for each popped number, store the **next greater** in the map
4. After processing `nums2`, loop through `nums1` and use the map to build the result array. If an element is not found in the map, assign **-1**

---

## 💻 Code (Java)

```java
import java.util.*;

class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Map<Integer, Integer> map = new HashMap<>();
        Stack<Integer> st = new Stack<>();
        int[] ans = new int[nums1.length];

        // Step 1: Build map for next greater element in nums2
        for (int num : nums2) {
            while (!st.isEmpty() && st.peek() < num) {
                map.put(st.pop(), num);
            }
            st.push(num);
        }

        // Step 2: Fill result for nums1 using the map
        for (int i = 0; i < nums1.length; i++) {
            ans[i] = map.getOrDefault(nums1[i], -1);
        }

        return ans;
    }
}
```

## 🧠 Intuition
Monotonic Stack helps efficiently track the next greater elements while traversing once

The HashMap keeps record of the next greater element for every number in nums2

For each element in nums1, we can directly access its next greater via map

## ⏱ Time and Space Complexity
Complexity	Value
Time	O(N + M)
Space	O(M) (map + stack)

Where:

N = nums1.length

M = nums2.length


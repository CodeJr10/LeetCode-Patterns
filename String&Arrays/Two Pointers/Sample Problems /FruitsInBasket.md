# 🍎🍌 Fruit Into Baskets

This problem involves collecting fruits from a row of trees, with a constraint of **only carrying two types of fruits at once** (like using two baskets).  
You must pick fruits from **a contiguous segment** of trees starting from any index, but once you pick a fruit of a third type, you must stop.

Your goal is to **return the maximum number of fruits you can collect**.

---

## 💡 Problem Statement

You are given an array `fruits` where `fruits[i]` represents the type of fruit on the `i-th` tree.

You have **two baskets**, and each basket can only hold **a single type of fruit**.

You must pick exactly one fruit from every tree (starting from any index), and can only stop when you pick a third fruit type.

Return the **length of the longest subarray** containing at most 2 distinct integers (fruit types).

---

## ✅ Sample Input & Output

### Example 1
Input: fruits = [1, 2, 1]
Output: 3
Explanation: You can collect all the fruits.

### Example 2
Input: fruits = [0, 1, 2, 2]
Output: 3
Explanation: Collect fruits [1, 2, 2]. You can’t pick 0 after that.

### Example 3
Input: fruits = [1, 2, 3, 2, 2]
Output: 4
Explanation: Collect fruits [2, 3, 2, 2].

---
## 🧠 Approach

We use the **Sliding Window** technique with a `HashMap` to keep track of the frequency of each fruit in the current window.

- Expand the window from the right by adding `fruits[right]` to the map.
- If the map has more than two distinct fruit types, start shrinking the window from the left.
- Always update the `maxLen` when the window is valid (i.e., contains at most 2 types).

---

## 🧾 Java Code

```java
class Solution {
    public int totalFruit(int[] fruits) {
        int left = 0;
        int right = 0;
        int maxLen = 0;
        Map<Integer, Integer> map = new HashMap<>();
        int k = 2;

        while (right < fruits.length) {
            int curr = fruits[right];
            map.put(curr, map.getOrDefault(curr, 0) + 1);

            while (map.size() > k) {
                int num = fruits[left];
                map.put(num, map.get(num) - 1);
                if (map.get(num) == 0) {
                    map.remove(num);
                }
                left++;
            }

            maxLen = Math.max(maxLen, right - left + 1);
            right++;
        }

        return maxLen;
    }
}
```

# ⏱️ Time & Space Complexity
⏰ Time Complexity: O(n)
Each element is visited at most twice — once by right and once by left.

# 📦 Space Complexity: O(k) → O(2)
Only 2 fruit types are stored in the map at any time.

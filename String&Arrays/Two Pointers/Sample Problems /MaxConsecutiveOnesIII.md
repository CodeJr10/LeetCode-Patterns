# 🔢 Max Consecutive Ones III

Given a binary array `nums` and an integer `k`, return the **maximum number of consecutive 1's** in the array if you can flip at most `k` 0's.

---

## 📥 Example

```
Input:  nums = [1,1,0,0,1,1,1,0], k = 2
Output: 7

Explanation:
Flip two 0's at indices 2 and 3 → becomes [1,1,1,1,1,1,1,0]
Max consecutive 1's = 7
```

---

## ✅ Approach: Sliding Window with At Most k Zero Flips

### 💡 Idea:
- Maintain a window `[left, right]` that contains **at most `k` zeroes**.
- Expand the window using `right`.
- If zeroes exceed `k`, shrink the window from the `left` to remove 0's.
- Track the maximum window length along the way.

---

### 📦 Code: (Java — Clean `while` Loop Version)

```java
class Solution {
    public int longestOnes(int[] nums, int k) {
        int left = 0, right = 0;
        int zeroes = 0, maxLen = 0;
        int n = nums.length;

        while (right < n) {
            if (nums[right] == 0) {
                zeroes++;
            }

            if (zeroes > k) {
                if (nums[left] == 0) {
                    zeroes--;
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

---

## ⏱️ Complexity Analysis

| Metric            | Value               |
|-------------------|---------------------|
| Time Complexity   | O(n) — single pass  |
| Space Complexity  | O(1) — constant vars|

---

## 🧪 More Test Cases

```
Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Output: 6
Explanation: Flip the two 0's at indices 4 and 5 → [1,1,1,0,0,1,1,1,1,1] → longest = 6

Input: nums = [0,0,1,1,1,0,0], k = 0
Output: 3

Input: nums = [1,0,1,1,0], k = 1
Output: 4
```

---

## 🧠 Concepts Covered
- Sliding Window
- Two Pointers
- Window Shrinking
- Binary Array Handling
---

## 🧩 Link ton LeetCode
- [Leetcode 1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)


# 🔢 Subarrays with K Different Integers

This problem focuses on identifying subarrays that contain **exactly K distinct integers** using an optimized sliding window technique.

---

## 🚀 Problem Description

Given an integer array `nums` and an integer `k`, you are to return the number of subarrays that contain **exactly** `k` distinct integers.

---

## 💡 Intuition

We transform the original problem into two simpler subproblems:

> 🔄 `subarraysWithKDistinct = atMost(k) - atMost(k - 1)`

Where:

- `atMost(k)` returns the number of subarrays with at most `k` distinct integers.
- Subtracting `atMost(k - 1)` leaves us with only the subarrays that contain **exactly k** distinct integers.

---

## 🧠 Approach

We apply the **sliding window** pattern and use a **HashMap** to keep track of character frequencies in the current window.

- Expand the window to the right by adding `nums[right]`.
- If the window contains more than `k` distinct numbers, shrink the window from the left until it's valid again.
- For every valid window, we add the number of subarrays ending at `right` (`right - left + 1`) to the count.

---

## ✅ Java Code

```java
class Solution {
    public int subarraysWithKDistinct(int[] nums, int k) {
        return findSubarrays(nums, k) - findSubarrays(nums, k - 1);
    }

    private int findSubarrays(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        int left = 0, right = 0, count = 0;

        while (right < nums.length) {
            int rightNumber = nums[right];
            map.put(rightNumber, map.getOrDefault(rightNumber, 0) + 1);

            while (map.size() > k) {
                int leftNumber = nums[left];
                map.put(leftNumber, map.get(leftNumber) - 1);
                if (map.get(leftNumber) == 0) {
                    map.remove(leftNumber);
                }
                left++;
            }

            count += right - left + 1;
            right++;
        }

        return count;
    }
}
```

## ⏱️ Time & Space Complexity
#### Time Complexity: O(n)

Each element is visited at most twice: once by the right pointer, once by the left pointer.

#### Space Complexity: O(k)

The map stores at most k elements (distinct integers in the current window).

## 📌 Notes
This pattern is a common trick for problems involving "exactly K" type conditions.

Subtracting atMost(k - 1) from atMost(k) gives the precise count for k.

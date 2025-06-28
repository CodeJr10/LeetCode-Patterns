# 📊 Number of Subarrays with Sum = K

This problem involves finding the number of **contiguous subarrays** whose elements sum up to a given integer `goal`.  
It is a classic application of **prefix sums** and **sliding window** for binary arrays (0s and 1s).

---

## 💡 Problem Summary

You're given a binary array `nums` and an integer `goal`.  
Return the number of **non-empty subarrays** that sum to exactly `goal`.

A subarray is a contiguous part of an array.

---

## 🧠 Approach

### Concept: Inclusion-Exclusion using Sliding Window

To count the number of subarrays with sum equal to `goal`, we:

1. Count the number of subarrays whose sum is **at most `goal`**
2. Count the number of subarrays whose sum is **less than `goal`**
3. Subtract the two to get the **number of subarrays with sum exactly equal to `goal`**

This is because:

Subarrays with sum == goal =
Subarrays with sum ≤ goal
Subarrays with sum < goal

We use a **sliding window** technique to count subarrays with sum ≤ `goal`.

---

## 🧾 Java Code

```java
class Solution {
    public int numSubarraysWithSum(int[] nums, int goal) {
        return numSubarraysWithSumLessThanGoal(nums, goal) 
             - numSubarraysWithSumLessThanGoal(nums, goal - 1);
    }

    private int numSubarraysWithSumLessThanGoal(int[] nums, int goal) {
        if (goal < 0) return 0;

        int left = 0, sum = 0, count = 0;

        for (int right = 0; right < nums.length; right++) {
            sum += nums[right];

            while (sum > goal) {
                sum -= nums[left++];
            }

            // All subarrays ending at right and starting from left to right are valid
            count += right - left + 1;
        }

        return count;
    }
}
```
## ⏱️ Time and Space Complexity
#### Time Complexity: O(n)

We iterate over the array once with two pointers left and right

#### Space Complexity: O(1)

Only variables used — no extra space beyond a few integers

---

🔍 Notes
This problem only works efficiently with arrays of non-negative integers (like binary arrays with 0 and 1).

This technique generalizes to problems where you're asked for exact sums using the atMost pattern.

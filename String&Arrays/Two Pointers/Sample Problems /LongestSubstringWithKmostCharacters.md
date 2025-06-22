# 🔤 Longest Substring with At Most K Distinct Characters

This problem is a classic variation of the sliding window pattern.

You're given a string `s` and an integer `k`. Your task is to find the **length of the longest substring** that contains **at most `k` distinct characters**.

---

## 💡 Problem Statement

Given a string `s` and an integer `k`, return the length of the longest substring that contains at most `k` distinct characters.

If `k` is 0, return 0 (no characters are allowed at all).

---
## 📘 Examples

### Example 1

Input: s = "eceba", k = 2  
Output: 3  
Explanation: The substring is "ece" with 2 distinct characters.

### Example 2
Input: s = "aa", k = 1  
Output: 2  
Explanation: The substring is "aa" with only 1 distinct character.

### Example 3
Input: s = "abaccc", k = 2  
Output: 4  
Explanation: The longest substring is "accc" with 2 distinct characters.

## 🧠 Approach

We use the **sliding window technique** along with a `HashMap<Character, Integer>` to track the frequency of characters in the current window:

1. Start with both `left` and `right` pointers at 0.
2. Move the `right` pointer one step at a time, expanding the window.
3. Insert the current character into the map and update its frequency.
4. If the map contains **more than `k` distinct characters**, shrink the window from the left until only `k` remain.
5. At each step, update the `maxLen` with the current window size.

---

## 🧾 Java Code

```java
class Solution {
    public int kDistinctChar(String s, int k) {
        int maxLen = 0;
        int left = 0;
        int right = 0;

        Map<Character, Integer> map = new HashMap<>();

        while (right < s.length()) {
            char rightChar = s.charAt(right);
            map.put(rightChar, map.getOrDefault(rightChar, 0) + 1);

            if (map.size() > k) {
                char leftChar = s.charAt(left);
                map.put(leftChar, map.get(leftChar) - 1);
                if (map.get(leftChar) == 0) {
                    map.remove(leftChar);
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
Time Complexity: O(n)
Both pointers (left, right) move at most n steps each.

Space Complexity: O(k)
At most k unique characters are stored in the map.

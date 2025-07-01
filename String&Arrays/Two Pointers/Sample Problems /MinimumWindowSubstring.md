# 🔍 Minimum Window Substring

This problem asks you to find the smallest window (substring) in string `s` that contains **all characters** from string `t`, including their counts.

---

## 💡 Problem Statement

Given two strings `s` and `t`, return the **minimum window** in `s` that contains all the characters in `t`. If no such window exists, return an empty string `""`.

You must include each character from `t` as many times as it appears.

---

## 🧠 Approach: Sliding Window + HashMap

We use a **sliding window** and a **HashMap** to keep track of the required characters from `t` and how many we’ve matched so far.

### Key Steps:

1. **Count characters in `t`**: Store in a HashMap `map<char, count>`.
2. **Expand the right pointer**:
   - If the character exists in the map, decrease its count.
   - If it's still needed (`map.get(char) >= 0`), increment `cnt`.
3. **Shrink from the left** while all characters from `t` are matched (`cnt == t.length()`).
4. Keep track of the **minimum window** during the process.

---

## ✅ Java Code

```java
class Solution {
    public String minWindow(String s, String t) {
        int n = s.length(); 
        int m = t.length();
        if (m > n) return "";

        int minLen = Integer.MAX_VALUE;
        int startIndex = -1;
        Map<Character, Integer> map = new HashMap<>();
        int left = 0, right = 0, cnt = 0;

        // ✅ Fill frequency map from string t
        for (int i = 0; i < m; i++) {
            char ch = t.charAt(i);
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }

        // ✅ Start sliding window
        while (right < n) {
            char curr = s.charAt(right);

            if (map.containsKey(curr)) {
                map.put(curr, map.get(curr) - 1);
                if (map.get(curr) >= 0) {
                    cnt++; // Only increment if char was needed
                }
            }

            // ✅ Try to shrink the window when all t's chars are included
            while (cnt == m) {
                if (right - left + 1 < minLen) {
                    minLen = right - left + 1;
                    startIndex = left;
                }

                char leftChar = s.charAt(left);
                if (map.containsKey(leftChar)) {
                    map.put(leftChar, map.get(leftChar) + 1);
                    if (map.get(leftChar) > 0) {
                        cnt--; // Only reduce cnt if char is needed again
                    }
                }

                left++;
            }

            right++;
        }

        return startIndex == -1 ? "" : s.substring(startIndex, startIndex + minLen);
    }
}
```
---
## ⏱️ Time & Space Complexity
### Time Complexity: O(n + m)

n is the length of s

m is the length of t

We process each character at most twice

### Space Complexity: O(m)

For the character count map of string t

---
## 🧪 Notes
This is a classic sliding window with character frequency tracking.

Edge case: if t.length() > s.length(), return empty string.

cnt only increases when the character is still needed (map.get(char) >= 0).

Use startIndex and minLen to track the smallest valid window.

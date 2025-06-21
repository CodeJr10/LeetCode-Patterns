# 🔠 Longest Substring Without Repeating Characters

Given a string `s`, return the **length of the longest substring** that contains **no repeating characters**.

---

## 📥 Example

```
Input:  s = "abcdabgeaz"
Output: 6

Explanation:
The longest substrings without repeating characters are:
- "abcd" → length 4
- "dabge" → length 5
- ✅ "abgeaz" → length 6
```

---

## ✅ Approach 1: Sliding Window Using `HashSet`

### 💡 Idea:
Use a **set** to keep track of unique characters.  
When a duplicate is found, shrink the window from the left until it's valid again.

### 📦 Code:

```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s.length() == 0) return 0;

        int l = 0;
        int maxLen = 0;
        Set<Character> set = new HashSet<>();

        for (int r = 0; r < s.length(); r++) {
            while (set.contains(s.charAt(r))) {
                set.remove(s.charAt(l));
                l++;
            }
            set.add(s.charAt(r));
            maxLen = Math.max(maxLen, r - l + 1);
        }

        return maxLen;
    }
}
```

### ⏱️ Complexity:

| Metric           | Value        |
|------------------|--------------|
| Time Complexity  | O(n)         |
| Space Complexity | O(k) → where `k` is the number of unique characters |

---

## ✅ Approach 2: Optimized Sliding Window Using `int[128]` (ASCII Only)

### 💡 Idea:
Instead of using a set, track character frequencies in a fixed-size array of 128 elements (assuming standard ASCII).

### 📦 Code:

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] freq = new int[128];
        int l = 0, maxLen = 0;

        for (int r = 0; r < s.length(); r++) {
            char curr = s.charAt(r);
            freq[curr]++;

            while (freq[curr] > 1) {
                freq[s.charAt(l)]--;
                l++;
            }

            maxLen = Math.max(maxLen, r - l + 1);
        }

        return maxLen;
    }
}
```

### ⏱️ Complexity:

| Metric           | Value               |
|------------------|---------------------|
| Time Complexity  | O(n)                |
| Space Complexity | O(1) → fixed array  |

---

## 🧠 Summary

| Feature               | `HashSet` Approach     | `int[128]` Array Approach |
|------------------------|-------------------------|----------------------------|
| Unicode support        | ✅ Yes                  | ❌ ASCII only              |
| Performance            | Good                    | ✅ Best for ASCII          |
| Memory efficiency      | Moderate (dynamic set)  | ✅ O(1) fixed-size array   |
| Use case               | Flexible                | Fastest for ASCII problems |

---

## 🧪 Test It Yourself

```
Input: "abcabcbb"      → Output: 3 ("abc")
Input: "bbbbb"         → Output: 1 ("b")
Input: "pwwkew"        → Output: 3 ("wke")
Input: "abba"          → Output: 2 ("ab")
Input: " "             → Output: 1
Input: ""              → Output: 0
```

---

## 📌 Notes

- If your input may include **Unicode characters** (e.g., emojis, non-ASCII symbols), prefer the `HashSet<Character>` solution.
- The array-based method is perfect when you're **sure** the string only includes ASCII characters (a-z, A-Z, 0–9, symbols).



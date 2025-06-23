# 🔤 Number of Substrings Containing All Three Characters

This problem asks you to count how many substrings contain **at least one occurrence** of each of the characters `'a'`, `'b'`, and `'c'`.

---

## 💡 Problem Description

Given a string `s` consisting only of the characters `'a'`, `'b'`, and `'c'`, your task is to count the number of substrings that contain **at least one occurrence of all three characters**.

---

## ✅ Examples
### Example 1
Input: "abcabc"
Output: 10

### Example 2
Input: "aaacb"
Output: 3

### Example 3
Input: "aabbcc"
Output: 4

---

## 🧠 Approach

We keep track of the **last seen index** of each of the characters `'a'`, `'b'`, and `'c'`.

### Key Observations:
- Any valid substring must end at a position `i` and contain all three characters.
- To compute how many such substrings end at index `i`, find the **minimum** among the last seen positions of `'a'`, `'b'`, and `'c'`.
- All substrings that start between index `0` and that **minimum position** (inclusive) and end at `i` are guaranteed to include all three characters.

---

## 🛠️ Implementation Details

- Use an integer array `latestPosition` of size 3 to store the last index where `'a'`, `'b'`, and `'c'` appeared.
  - Index `0` → `'a'`
  - Index `1` → `'b'`
  - Index `2` → `'c'`
- Initialize all values to `-1` (meaning not seen yet).
- For every character in the string:
  - Update its last seen index in `latestPosition`.
  - Find the **minimum** value in `latestPosition`.
  - Add `minPosition + 1` to the result (since all substrings from `0` to `minPosition` ending at `i` are valid).

---

## ✅ Java Code

```java
class Solution {
    public int numberOfSubstrings(String s) {

        int[] latestPosition = new int[] {-1, -1, -1};
        int answer = 0;

        for (int i = 0; i < s.length(); ++i) {
            char currentChar = s.charAt(i);
            
            // Update the latest index of the current character
            latestPosition[currentChar - 'a'] = i;

            // Get the earliest index among the three characters
            int minPosition = Math.min(latestPosition[0], 
                                Math.min(latestPosition[1], latestPosition[2]));
            
            // If all three characters have been seen, count substrings
            answer += minPosition + 1;
        }

        return answer;
    }
}
```
# ⏱️ Time & Space Complexity

### Time Complexity: O(n)

We loop over the string once. All operations inside the loop are constant time.

### Space Complexity: O(1)

Only a fixed-size array of length 3 is used.

# 📌 Notes
This method avoids generating or checking all substrings explicitly, making it much more efficient.

Works only for strings with exactly three distinct characters (specifically 'a', 'b', 'c'). For general cases with more distinct characters, the code would need adjustment.

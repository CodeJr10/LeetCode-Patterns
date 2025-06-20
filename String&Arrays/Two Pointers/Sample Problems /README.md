# 🃏 Maximum Points You Can Obtain from Cards

Given `N` cards arranged in a row, each card has a score (represented by the `cardScore` array).  
You are allowed to choose exactly `k` cards, and in each step, you may pick a card from either the **beginning** or the **end** of the row.  
Return the **maximum score** that can be obtained.

---

## 📥 Examples

### 1️⃣ Example 1

**Input:**  
`cardScore = [1, 2, 3, 4, 5, 6]`, `k = 3`  

**Output:**  
`15`

**Explanation:**  
Choosing the rightmost cards will maximize your total score.  
The optimal cards chosen are the last three: `4`, `5`, `6`.  
So the score is:  
`4 + 5 + 6 = 15`

---

### 2️⃣ Example 2

**Input:**  
`cardScore = [5, 4, 1, 8, 7, 1, 3]`, `k = 3`  

**Output:**  
`12`

**Explanation:**  
- Step 1: Pick from the beginning → `5`  
- Step 2: Pick from the beginning → `4`  
- Step 3: Pick from the end → `3`  

Total score = `5 + 4 + 3 = 12`

---

## ✅ Java Solution

```java
class Solution {
    public int maxScore(int[] cardScore, int k) {
        int Lsum = 0;
        int Rsum = 0;
        int n = cardScore.length;

        // Step 1: Get the sum of the first k cards from the left
        for (int i = 0; i < k; i++) {
            Lsum += cardScore[i];
        }

        int maxSum = Lsum;

        // Step 2: Shift cards one by one from left to right and update the max
        for (int i = 0; i < k; i++) {
            Lsum -= cardScore[k - 1 - i];      // Remove one from left
            Rsum += cardScore[n - 1 - i];      // Add one from right
            maxSum = Math.max(maxSum, Lsum + Rsum);
        }

        return maxSum;
    }
}
```

---

## 📊 Complexity

- 🧠 **Approach:** Sliding Window (Left-to-Right Swap)
- ⏱ **Time Complexity:** `O(k)`
- 📦 **Space Complexity:** `O(1)`

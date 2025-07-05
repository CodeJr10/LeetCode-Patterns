# 🔁 Postfix to Infix Conversion

## 🧠 Problem Statement

Given a **postfix expression**, convert it into its equivalent **infix expression**.

In **postfix notation**, operators follow their operands (e.g., `AB+`).  
In **infix notation**, the operator is written between operands with parentheses (e.g., `(A+B)`).

---

## 🧾 Example

### ✅ Example 1
Input: AB+
Output: (A+B)

shell
Copy
Edit

### ✅ Example 2
Input: ABC/-AK/L-*
Output: ((A-(B/C))*((A/K)-L))

pgsql
Copy
Edit

---

## 🧩 Explanation

To convert a **postfix** expression to **infix**:

1. Initialize an empty stack of strings.
2. Traverse the postfix string from **left to right**.
3. For each character:
   - If it’s an **operand**, push it to the stack.
   - If it’s an **operator**:
     - Pop the **top two operands** from the stack.
     - Combine them into an infix expression in the format: `(operand1 operator operand2)`
     - Push the result back into the stack.
4. At the end, the only element in the stack is the final **infix expression**.

---

## 🧱 Java Code

```java
class Solution {
    static String postToInfix(String exp) {
        Stack<String> st = new Stack<>();

        for (int i = 0; i < exp.length(); i++) {
            char c = exp.charAt(i);

            if (Character.isLetterOrDigit(c)) {
                st.push(Character.toString(c));
            } else {
                String top = st.pop();
                String second = st.pop();
                String ans = "(" + second + c + top + ")";
                st.push(ans);
            }
        }

        return st.pop();
    }
}
```
---

## ⏱️ Time and Space Complexity

#### Time Complexity	O(N)
#### Space Complexity	O(N) (stack)

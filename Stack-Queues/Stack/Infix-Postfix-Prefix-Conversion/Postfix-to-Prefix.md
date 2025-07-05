# 🔁 Postfix to Prefix Expression Converter

This Java program converts a given **postfix (Reverse Polish Notation)** expression into its equivalent **prefix (Polish Notation)** form.

---

## 🧠 What is Postfix?

In **postfix notation**, the operator is written **after** the operands.

> 📌 Example:  
> `AB+` → `A + B`  
> `AB+CD-*` → `(A + B) * (C - D)`

It is stack-friendly and avoids parentheses.

---

## 🧠 What is Prefix?

In **prefix notation**, the operator is written **before** its operands.

> 📌 Example:  
> `+AB` → `A + B`  
> `*-+ABCD` → `((A + B) - C) * D`

Prefix notation is used in compilers and parsing because it's easy to evaluate without precedence rules.

---

## 🔁 Conversion Logic: Postfix ➡️ Prefix

### ✅ Steps:

1. **Traverse the postfix expression from left to right.**
2. **If the character is an operand**, push it onto the stack.
3. **If the character is an operator**:
   - Pop two operands from the stack.
   - Combine them as: `operator + operand1 + operand2`
   - Push the resulting expression back onto the stack.
4. Repeat until the end.
5. Final expression in the stack is the **prefix** result.

---

## ✅ Java Code

```java
import java.util.Stack;

class Solution {
    static String postToPre(String post_exp) {
        Stack<String> st = new Stack<>();

        for (int i = 0; i < post_exp.length(); i++) {
            char c = post_exp.charAt(i);

            if (Character.isLetterOrDigit(c)) {
                st.push(Character.toString(c)); // Push operand
            } else {
                // Pop two operands
                String op1 = st.pop();
                String op2 = st.pop();

                // Form prefix expression: operator + operand2 + operand1
                String ans = c + op2 + op1;
                st.push(ans);
            }
        }

        return st.pop(); // Final result
    }

    public static void main(String[] args) {
        String postfix = "AB+CD-*";
        System.out.println("Prefix: " + postToPre(postfix)); // Output: *+AB-CD
    }
}
```

---

## 🧪 Examples
🔹 Example 1
Input:
AB+

Output:
+AB

Explanation:
Postfix AB+ → infix A + B → prefix +AB

🔹 Example 2
Input:
AB+CD-*

Output:
*-+ABCD

Explanation:
Postfix (A + B) * (C - D) → prefix *-+ABCD

🔹 Example 3
Input:
AB^

Output:
^AB

Explanation:
Postfix AB^ → infix A ^ B → prefix ^AB

---
## ⏱️ Time & Space Complexity
Metric	Value
⏳ Time Complexity	O(N)
💾 Space Complexity	O(N)

Where N is the length of the postfix expression.

---
## 📌 Notes
Only single-character operands are supported in this basic version.

For multi-digit numbers or variables, a tokenized approach would be required.

This approach works best when the postfix expression is valid and complete.


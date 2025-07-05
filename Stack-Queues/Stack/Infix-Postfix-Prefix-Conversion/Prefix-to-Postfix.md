# 🔁 Prefix to Postfix Expression Converter

This Java program converts a given **prefix (Polish Notation)** expression into its equivalent **postfix (Reverse Polish Notation)** form.

---

## 🧠 What is Prefix?

In **prefix notation**, also known as **Polish notation**, the operator appears **before** its operands.

> 📌 Example:  
> `+AB` → `A + B`  
> `*-+ABCD` → `((A + B) - C) * D`

This notation avoids parentheses but is difficult for humans to parse directly.

---

## 🧠 What is Postfix?

In **postfix notation**, also known as **Reverse Polish notation**, the operator comes **after** its operands.

> 📌 Example:  
> `AB+` → `A + B`  
> `AB+CD-*` → `(A + B) * (C - D)`

Postfix is easy to evaluate using a stack-based machine and does not require parentheses.

---

## 🔁 Conversion Logic: Prefix ➡️ Postfix

### ✅ Steps:

1. **Traverse the prefix expression from right to left.**
2. **If the character is an operand** (letter or digit), push it onto a stack.
3. **If the character is an operator**:
   - Pop two operands from the stack.
   - Create a postfix string by placing the two operands first, then the operator: `operand1 + operand2 + operator`
   - Push the result back to the stack.
4. **Repeat** until the entire prefix expression is processed.
5. The final result on the top of the stack is the postfix expression.

---

## ✅ Java Code

```java
import java.util.Stack;

class Solution {
    static String preToPost(String pre_exp) {
        Stack<String> st = new Stack<>();

        for (int i = pre_exp.length() - 1; i >= 0; i--) {
            char c = pre_exp.charAt(i);

            if (Character.isLetterOrDigit(c)) {
                st.push(Character.toString(c)); // Push operand
            } else {
                // Pop two operands
                String op1 = st.pop();
                String op2 = st.pop();

                // Combine in postfix order: operand1 + operand2 + operator
                String ans = op1 + op2 + c;
                st.push(ans);
            }
        }

        return st.pop(); // Final result
    }

    // Optional test
    public static void main(String[] args) {
        String prefix = "*+AB-CD";
        System.out.println("Postfix: " + preToPost(prefix)); // Output: AB+CD-*
    }
}

```
---
## 🧪 Examples
🔹 Example 1
Input:
+AB

Output:
AB+

Explanation:
Prefix +AB → infix A + B → postfix AB+

🔹 Example 2
Input:
*-+ABCD

Output:
AB+CD-*

Explanation:
Prefix *-+ABCD → infix ((A + B) - C) * D → postfix AB+CD-*

🔹 Example 3
Input:
^AB

Output:
AB^

Explanation:
Prefix ^AB → infix A ^ B → postfix AB^

---
## ⏱️ Time & Space Complexity

⏳ Time Complexity	O(N)
💾 Space Complexity	O(N)

Where N is the length of the prefix expression.

---
## 📌 Notes
This implementation assumes all operands are single-character alphanumeric symbols.

For complex multi-digit operands or function calls, tokenization would be needed.

Prefix and postfix notations are parenthesis-free and ideal for compiler design and expression evaluation using stacks.


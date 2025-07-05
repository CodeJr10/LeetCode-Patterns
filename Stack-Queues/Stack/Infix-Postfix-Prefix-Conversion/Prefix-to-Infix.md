# 🔁 Prefix to Infix Expression Converter

This Java program converts a given **prefix (Polish notation)** expression into its equivalent **infix notation**.

---

## 🧠 What is Prefix?

In **prefix notation**, the operator comes **before** the operands:

+AB → A + B
*+AB-CD → (A + B) * (C - D)

This form is easier for computers to parse and evaluate **without parentheses**.

---

## 🧠 What is Infix?

In **infix notation**, the operator is placed **between** operands:

A + B
(A + B) * (C - D)

Infix is human-friendly but requires rules like operator precedence and parentheses for correct evaluation.

---

## 🔁 Conversion Logic

To convert from prefix ➡️ infix:

1. **Scan the prefix expression from right to left.**
2. **If the character is an operand**, push it to a stack.
3. **If the character is an operator**:
   - Pop two operands from the stack.
   - Combine them into an infix expression with parentheses: `(operand1 operator operand2)`
   - Push the result back to the stack.
4. After processing all characters, the stack will contain the full infix expression.

---

## ✅ Java Code

```java
import java.util.Stack;

class Solution {
    static String preToInfix(String pre_exp) {
        Stack<String> st = new Stack<>();
        
        // Start scanning from the end
        for (int i = pre_exp.length() - 1; i >= 0; i--) {
            char c = pre_exp.charAt(i);

            if (Character.isLetterOrDigit(c)) {
                st.push(Character.toString(c)); // Operand goes directly into stack
            } else {
                // Pop two operands
                String op1 = st.pop();
                String op2 = st.pop();

                // Combine them with operator
                String ans = "(" + op1 + c + op2 + ")";
                st.push(ans); // Push back the result
            }
        }

        // Final expression will be the only element in the stack
        return st.pop();
    }

    // Optional main for testing
    public static void main(String[] args) {
        String prefix = "*+AB-CD";
        System.out.println("Infix: " + preToInfix(prefix));  // Output: ((A+B)*(C-D))
    }
}
```
---

## ⏱️ Complexity
#### Time Complexity: O(N) – where N is the length of the prefix expression

#### Space Complexity: O(N) – for using the stack to build expressions

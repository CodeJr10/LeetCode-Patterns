# 🧮 Infix to Postfix Expression Converter

This repository provides a Java implementation to convert a **mathematical expression written in infix notation** into **postfix notation (Reverse Polish Notation)**.

---

## 📌 What is Infix?

Infix is the standard form of writing mathematical expressions that humans usually use:

A + B
(A * B) / Q

yaml
Copy
Edit

However, infix notation requires rules of **operator precedence**, **associativity**, and **parentheses** to determine the evaluation order — making it complex for computers to parse.

---

## 📌 What is Postfix?

Postfix (or Reverse Polish Notation) places operators **after** operands:

A B +
A B * Q /

csharp
Copy
Edit

Postfix removes the need for parentheses and makes evaluation easier and faster using a stack.

---

## 🧠 Algorithm: Infix ➡️ Postfix

To convert an infix expression to postfix:

1. Scan the infix expression from left to right.
2. If the scanned character is an **operand**, add it to the result.
3. If the scanned character is an **operator**:
   - While the stack is not empty and the precedence of the current operator is **less than or equal to** the precedence of the operator on top of the stack, **pop** from stack and add to result.
   - Push the current operator to the stack.
4. If the character is **'('**, push to stack.
5. If the character is **')'**, pop from stack to result until '(' is found. Discard both parentheses.
6. After scanning the expression, **pop all remaining operators** from the stack to the result.

---

## ✅ Java Code

```java
import java.util.Stack;

public class InfixToPostfix {

    // Function to return operator precedence
    static int precedence(char ch) {
        switch (ch) {
            case '+':
            case '-': return 1;
            case '*':
            case '/': return 2;
            case '^': return 3;
        }
        return -1;
    }

    // Main function to convert infix to postfix
    public static String infixToPostfix(String exp) {
        StringBuilder result = new StringBuilder();
        Stack<Character> stack = new Stack<>();

        for (int i = 0; i < exp.length(); i++) {
            char c = exp.charAt(i);

            // Operand → directly to result
            if (Character.isLetterOrDigit(c)) {
                result.append(c);
            }

            // Opening bracket → push to stack
            else if (c == '(') {
                stack.push(c);
            }

            // Closing bracket → pop till '('
            else if (c == ')') {
                while (!stack.isEmpty() && stack.peek() != '(') {
                    result.append(stack.pop());
                }
                stack.pop(); // discard '('
            }

            // Operator → check precedence
            else {
                while (!stack.isEmpty() && precedence(c) <= precedence(stack.peek())) {
                    result.append(stack.pop());
                }
                stack.push(c);
            }
        }

        // Pop remaining operators
        while (!stack.isEmpty()) {
            if (stack.peek() == '(') return "Invalid Expression";
            result.append(stack.pop());
        }

        return result.toString();
    }

    // Example usage
    public static void main(String[] args) {
        String expression = "a+b*(c^d-e)^(f+g*h)-i";
        System.out.println("Infix:   " + expression);
        System.out.println("Postfix: " + infixToPostfix(expression));
    }
}
```
---
## ⏱️ Complexity
#### Time Complexity: O(N) – where N is the length of the expression.

##### Space Complexity: O(N) – for the stack.

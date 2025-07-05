# 🧠 Infix to Prefix Expression Converter

This repository provides a Java implementation to convert a **mathematical expression written in infix notation** into **prefix notation (Polish Notation)**.

---

## 📌 What is Infix?

Infix is the human-readable way to write math expressions:

A + B
(A * B) / Q

But infix expressions require **operator precedence**, **associativity**, and parentheses to determine evaluation order, which makes them harder for computers to evaluate directly.

---

## 📌 What is Prefix?

Prefix notation places the **operator before the operands**:

A B
/ * A B Q

Prefix does **not require parentheses** because the position of operators directly determines the order of evaluation.

---

## 🔄 How Infix ➡️ Prefix Works

To convert infix to prefix:

1. **Reverse the infix expression.**
2. **Swap** all `(` with `)` and vice versa.
3. **Convert the modified expression to postfix.**
4. **Reverse** the postfix result to get prefix.

---

## ✅ Java Code

```java
import java.util.*;

public class InfixToPrefix {

    // Function to return precedence
    public static int prec(char ch) {
        switch (ch) {
            case '+': case '-': return 1;
            case '*': case '/': return 2;
            case '^': return 3;
        }
        return -1;
    }

    // Function to convert infix to prefix
    public static String infixToPrefix(String str) {
        // Step 1: Reverse the string
        StringBuilder s = new StringBuilder(str).reverse();

        // Step 2: Swap ( and )
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') s.setCharAt(i, ')');
            else if (s.charAt(i) == ')') s.setCharAt(i, '(');
        }

        // Step 3: Convert to postfix
        Stack<Character> st = new Stack<>();
        StringBuilder ans = new StringBuilder();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (Character.isLetterOrDigit(c)) {
                ans.append(c);
            } else if (c == '(') {
                st.push(c);
            } else if (c == ')') {
                while (!st.isEmpty() && st.peek() != '(') {
                    ans.append(st.pop());
                }
                st.pop(); // Discard '('
            } else if (c == '^') {
                st.push(c); // Right associative
            } else {
                while (!st.isEmpty() && prec(c) < prec(st.peek())) {
                    ans.append(st.pop());
                }
                st.push(c);
            }
        }

        // Step 4: Pop remaining operators
        while (!st.isEmpty()) {
            ans.append(st.pop());
        }

        // Step 5: Reverse result for prefix
        return ans.reverse().toString();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter infix expression: ");
        String infix = sc.nextLine();

        String prefix = infixToPrefix(infix);
        System.out.println("Prefix Expression: " + prefix);

        sc.close();
    }
}
```

----
Input  : (a+b)*c <br>
Output : *+abc

Input  : a+b*(c^d-e)^(f+g*h)-i <br>
Output : -+a*b^-^cde+f*ghi

---

## ⏱️ Complexity
Time Complexity: O(N) – scanning and reversing the string

Space Complexity: O(N) – for the stack and output


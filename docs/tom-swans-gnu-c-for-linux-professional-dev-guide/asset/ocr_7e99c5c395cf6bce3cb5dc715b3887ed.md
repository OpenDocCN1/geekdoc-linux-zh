# ASSOCIATIVITY AND PRECEDENCE

When it evaluates an expression, C++ applies operators to operands in either left-to-right or right-to-left order, a property known as associativity. Most expressions evaluate operands in left to right order, but some go the other way—assignments, for example, evaluate from right to left.

Precedence dictates which operators apply before others. In complex expressions, subexpressions with operators of higher precedence evaluate before subexpressions with operators of lower precedence. Appendix B, “C++ Operator Precedence and Associativity,” documents these characteristics for all C and C++ operators, many of which you meet in this and other chapters.

From Appendix B, it’s evident that multiplication and division have higher precedence than addition and subtraction (see levels 4 and 5 in Appendix B). Always consider such facts. For example, consider this expression:

```
A + B * C - D
```

Because multiplication has higher precedence than addition and subtraction, C++ evaluates the expression by first multiplying B times C. It then adds A to the subexpression’s result, after which it subtracts D. The addition is performed before the subtraction in this case because, although operators + and - are equal in precedence, their associativity is left to right. Use parentheses to override the default precedence. For example, C++ evaluates the following expression differently:

```
(A + B) * (C - D)
```

Although the expression employs the same operators and operands as before, because parentheses have the highest precedence over all operators (see level 1 in Appendix B), C++ evaluates the subexpressions (A + B) and (C - D) first. It then multiplies the results of those subexpressions giving, for most input values, very different results than in the absence of parentheses.

In most expressions, common sense and a good helping of parentheses are your best guides to accurate results. You don’t need to memorize lots of precedence and associativity rules to understand the evaluation order of expressions such as this:

```
y = ((a * x) + b) / (x + c);
```

Even though the purpose of the formula might not be obvious (it describes a hyperbolic curve, in case you’re interested), the parentheses make perfectly clear which subexpressions belong together. Relying on operator precedence to produce a correct answer, you could write the preceding statement as

```
y = (a * x + b) / (x + c);
```

Because multiplication and division associate from left to right, one set of parentheses in the former expression isn’t needed. Even so, the extra parentheses make the expression perfectly clear, and they cost nothing in performance.
# THE MIN AND MAX OPERATORS

Newer releases of ANSI C++ compilers, including GNU C++, add two additional operators that many programmers don’t even know exist. Use the lesser-of and greater-of operators to compare two values, usually in an assignment. They are also known as the min and max operators. For example, given two integers value1 and value2 (they can be values of other fundamental types), the following statement assigns the lesser value to result:

```
result = value1 <? value2; // Assign lesser value to result
```

Similarly, the following statement assigns the greater of the two values to result:

```
result = value1 >? value2; // Assign greater value to result
```

The order of variables in the expressions to the right of the assignment doesn’t matter. If value1 equals value2, result is set to that value.

# SUMMARY

All expressions have values. Even a simple variable name such as counter is an expression that has a value. With operators, programs create complex expressions that perform calculations and comparisons. Use parentheses to group subexpressions and force a different evaluation order. In the absence of parentheses, C++ evaluates expressions based on operator precedence and associativity, as detailed in Appendix B.

For more information on subjects introduced in this chapter, turn to the following chapters:

+   - Chapter 9, “Controlling Program Flow”
+   - Chapter 10, “Creating and Calling Functions”
+   - Chapter 11, “Managing Memory with Pointers”
+   - Chapter 22, “Mastering the Standard string Class”
+   - Appendix B, “C++ Operator Precedence and Associativity”
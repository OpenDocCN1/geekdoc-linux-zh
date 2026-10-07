# Appendix B: Built-In Command Reference

-expression Bit-wise negation.

+   * expression * expression Multiplication.

expression / expression Division.

expression % expression Remainder of 1st expression after division by the 2nd expression.

+   * expression + expression Addition.

expression - expression Subtraction.

+   * expression << expression Left shift first expression by the number of bits given by the second expression.

expression >> expression Right shift expression by the number of bits given by the second expression.

+   * expression <= expression Less than or equal to.

expression >= expression Greater than or equal to.

expression < expression Less than.

expression > expression Greater than.

+   * expression == expression Equal.

expression != expression Not equal to.

+   * expression & expression Bit-wise OR. Both expressions are always evaluated.

+   * expression ^ expression Bit-wise Exclusive OR.

+   * expression | expression Bit-wise OR. Both expressions are always evaluated.

+   * expression && expression Logical AND. If the first expression is non-zero, then the second expression is not evaluated.

+   * expression || expression Logical OR. If the first expression is non-zero, then the second expression is not evaluated.

+   * expression ? expression: expression Conditional operator. If the first expression is non-zero, then the second expression is evaluated. Otherwise the third expression is evaluated.
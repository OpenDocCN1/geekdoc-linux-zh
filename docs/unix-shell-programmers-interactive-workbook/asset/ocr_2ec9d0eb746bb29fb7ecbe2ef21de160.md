# Appendix B: Built-In Command Reference 557

ksh performs all calculations using the double precision floating point arithmetic type on your system. ksh does not check for overflow.

A floating point constant has the form ([number].[number][exponent]), where number is any non-negative decimal, and exponent is E or optionally followed by + - and a non-negative decimal number.

An integer constant has the form [base]#number, where base is a decimal integer between 2 and 64 that defines the arithmetic base (default is 10), and number is any non-negative number.

A variable is denoted by a *. If in an arithmetic expression has the integer attribute, then ksh uses the value of the variable. Otherwise, ksh assumes that

the value of the variable is an arithmetic expression, and tries to evaluate it.

An arithmetic function is denoted by function(expression), where function is one of the following: abs (absolute value), acos (arc cosine of angle in radians), asin (arc sine), atan (arc tangent), cos (cosine),cosh (hyperbolic cosine), exp (exponential with base e (2.718281828459045)), int (greatest integer less than or equal to value of expression), log (logarithm base), sin (sine), sinh (hyperbolic sine), sqrt (square root), tan (tangent), tanh (hyperbolic tangent).

An expression is a constant, a variable, or is constructed with the following operators. The value of an expression with a comparison operator or a logical operator is 1 if non-zero (true) or 0 (false) otherwise. Operators are listed in order of precedence, with the highest ones first. Items of the same precedence are listed under the same base. ksh evaluates all items of the same precedence left-to-right, except for = and op= and other assignment operators, which it evaluates right-to-left.

+   * (expression)

+   * varname/++idname

+   * varname--idname

+   * +expression

+   * -expression

+   * !expression

Overrides precedence rules.

Postfix/prefix increment.

Postfix/prefix decrement.

Unary plus.

Unary minus.

Logical negation. The value is 0 for any expression whose value is 0.
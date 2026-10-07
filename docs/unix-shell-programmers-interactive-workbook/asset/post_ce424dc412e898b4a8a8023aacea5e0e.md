
# 556 Appendix B: Built-In Command Reference

to unpredictable results. For more information: see Chapter 1 (Setting Up.)

# { ... } BRACE GROUPING OPERATOR

{ compound-list }

ksh runs compound-list in the current environment. The return value is the return value of the last command in compound-list. For more information: see Chapter 3 (Compound Command Syntax).

# ( ...) SUBSHELL GROUPING OPERATOR

( compound-list )

ksh runs compound-list in a subshell environment. For more information: see Chapter 3 (Compound Command Syntax).

# ( ...) ARRAY INITIALIZATION

```
varname=( value ... )
varname=( ([expression]=value ... )
varname=(assignment ... )
```

The first form assigns values to the indexed array varname, starting with index position 0.

The second form assigns values to the associative array varname using expression as the array subscript.

The third form assigns values to a set of variables whose names are of the form varname.name, where name is the left-hand side of an assignment. typeset commands are allowed in assignments provided they are separated by semicolons or newlines. For more information: see Chapter 6 (Advanced Variable Usage).

# (( )) ARITHMETIC COMMAND

```
(( word ... ))
```

ksh does command substitution, parameter expansion, arithmetic expansion, and quote removal for each word to generate an arithmetic expression that is evaluated as follows:

# Appendix B: Built-In Command Reference 557

ksh performs all calculations using the double precision floating point arithmetic type on your system. ksh does not check for overflow.

A floating point constant has the form ([number].[number][exponent]), where number is any non-negative decimal, and exponent is E or optionally followed by + - and a non-negative decimal number.

An integer constant has the form [base]#number, where base is a decimal integer between 2 and 64 that defines the arithmetic base (default is 10), and number is any non-negative number.

A variable is denoted by a *. If in an arithmetic expression has the integer attribute, then ksh uses the value of the variable. Otherwise, ksh assumes that the value of the variable is an arithmetic expression, and tries to evaluate it.

An arithmetic function is denoted by function(expression), where function is one of the following: abs (absolute value), acos (arc cosine of angle in radians), asin (arc sine), atan (arc tangent), cos (cosine),cosh (hyperbolic cosine), exp (exponential with base e (2.718281828459045)), int (greatest integer less than or equal to value of expression), log (logarithm base), sin (sine), sinh (hyperbolic sine), sqrt (square root), tan (tangent), tanh (hyperbolic tangent).

An expression is a constant, a variable, or is constructed with the following operators. The value of an expression with a comparison operator or a logical operator is 1 if non-zero (true) or 0 (false) otherwise. Operators are listed in order of precedence, with the highest ones first. Items of the same precedence are listed under the same base. ksh evaluates all items of the same precedence left-to-right, except for = and op= and other assignment operators, which it evaluates right-to-left.

- * (expression)
- * varname/++idname
- * varname--idname
- * +expression
- * -expression
- * !expression
Overrides precedence rules.

Postfix/prefix increment.

Postfix/prefix decrement.

Unary plus.

Unary minus.

Logical negation. The value is 0 for any expression whose value is 0.

- -expression Bit-wise negation.

- * expression * expression Multiplication.
- expression / expression Division.
- expression % expression Remainder of 1st expression after division by the 2nd expression.
- * expression + expression Addition.
- expression - expression Subtraction.
- * expression << expression Left shift first expression by the number of bits given by the second expression.
- expression >> expression Right shift expression by the number of bits given by the second expression.
- * expression <= expression Less than or equal to.
- expression >= expression Greater than or equal to.
- expression < expression Less than.
- expression > expression Greater than.
- * expression == expression Equal.
- expression != expression Not equal to.
- * expression & expression Bit-wise OR. Both expressions are always evaluated.
- * expression ^ expression Bit-wise Exclusive OR.
- * expression | expression Bit-wise OR. Both expressions are always evaluated.
- * expression && expression Logical AND. If the first expression is non-zero, then the second expression is not evaluated.
- * expression || expression Logical OR. If the first expression is non-zero, then the second expression is not evaluated.
- * expression ? expression: expression Conditional operator. If the first expression is non-zero, then the second expression is evaluated. Otherwise the third expression is evaluated.

# Appendix B: Built-In Command Reference 559

- - varname = expression
Assignment.

- - varname op = expression
Compound assignment. The is equivalent to varname = varname expression. op must be * / % + - << >> ^ or |
- - expression, expression
Comma operator. Both expressions are evaluated. The resulting value is the value of the second expression.

For more information: see Chapter 6 (Advanced Variable Usage).

# [ ... ] LEFT BRACKET COMMAND

```
[ expression ]
```
test [expression]

# [[ ]] CONDITIONAL COMMAND

```
[[ test-expression ]]
```

The [[ ]] makes test and some obsolete.

The following are listed in order of precedence, from highest to lowest:
- (test-expression)
Evaluates to value of test-expression.

- ! test-expression
Logical negation of test-expression.

- test-expression && test-expression
Evaluates to True if both test expressions are True. The second test expression is expanded only if the first test expression is True.

- test-expression || test-expression
Evaluates to True if either of the test expressions are True. The second test expression is expanded only if the first test expression is False.

# Appendix B: Built-In Reference 59

Conditional expression primitives are unary and binary expressions that evaluate to True or False. Spaces or tabs are required to separate operators from operands.

- -e file: True if file exists.
- -a file: True if file exists. Do not use this primitive; use -e instead.
- -r file: True if file exists and is readable.
- -w file: True if file exists and is writable. file will not be writable on a readonly system even if this test indicates True.
- -x file: True if file exists and is executable. If file is a directory, True indicates that the directory can be searched.
- -f file: True if file exists and is a regular file.
- -d file: True if file exists and is a directory.
- -c file: True if file exists and is a character special file.
- -b file: True if file exists and is a block special file.
- -p file: True if file exists and is a named pipe (fifo).
- -u file: True if file exists and its set-user-id bit is set.
- -g file: True if file exists and its set-group-id bit is set.
- -k file: True if file exists and its sticky bit is set.
- -s file: True if file exists and has a size greater than zero.
- -L file: True if file exists and is a symbolic link.
- -h file: True if file exists and is a symbolic link.
- -O file: True if file exists and its owner is the effective user id.
- -G file: True if file exists and its group is the effective group id.
- -S file: True if file exists and is a special file of type socket.
- -t fildes: True if the file whose descriptor number is file is open and associated with a terminal device.
- -nt file2: True if file1 is newer than file2 or if file2 does not exist.
- -ot file2: True if file1 is older than file2 or if file2 does not exist.

# Arithmetic Expressions

General Format: $ ( (expression) )

The shell evaluates the integer arithmetic expression. expression can contain constants, shell variables (which don't have to be preceded by dollar signs), and operators. The operators, in order of decreasing precedence, are

+   - unary minus
- bitwise NOT
- logical negation
- multiplication, division, remainder
- addition, subtraction
- left shift, right shift
- comparison
- equal, not equal
- bitwise AND
- bitwise exclusive OR
- bitwise OR
- logical AND
- logical OR

expr1 ? expr2 : expr3

conditional operator

=, *, /=, %
+=, <<=, >>=\n&=, ^=, |=

assignment

Parentheses may be used to override operator precedence.

The exit status is zero (true) if the last expression is nonzero and one (false) if the last expression is zero.

The C operators sizeof, ++ and -- may be available in your shell implementation but are not required by the standard. Check by typing sizeof and see what happens.

Examples

```
y=$((22 * 33))
z=$((y * y / (y - 1)))
```
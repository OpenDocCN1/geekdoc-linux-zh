# expr

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwhfss |

# See Also

share(1M), shareall(1M), unshare(1M), unshareall(1M), attributes(5)

# expr — Evaluate Arguments as an Expression

# Synopsis

```
/usr/bin/expr argument...
/usr/xpg/bin/expr argument...
/usr/ucb/expr argument...
```

# Description

The expr command evaluates the expression and writes the result to standard output. Each token of the expression is a separate argument, you must separate terms of the expression by blanks. Quote strings containing blanks or other special characters. You can precede integer-valued arguments by a unary minus sign. Escape characters special to the shell. The length of the expression is limited to LINE_MAX (2048 characters).

> Note — The character 0 is written to indicate a zero value and nothing is written to a null string.

# Operands

Evaluated as an expression. Separate terms of the expression with blanks. You must escape characters special to the shell (see sh(1)). Quote strings containing blanks or special characters. The length of the expression is limited to LINE_MAX (2048 characters).

The operators and keywords are listed below. The list is in order of increasing precedence, with equal precedence operators grouped within {} symbols. All of the operators are left-associative.

```
expr | expr
```

Return the first expr if it is neither null nor 0; otherwise, return the second expr.

```
expr & expr
```

Return the first expr if expr is neither null or 0; otherwise, return 0.
# Arithmetic Expansion

The shell allows arithmetic to be performed by expansion. This allow us to use the shell prompt as a calculator:

```
[me@linuxbox ~]$ echo $((2 + 2))
4
```

Arithmetic expansion uses the form:

```
$((expression))
```

where expression is an arithmetic expression consisting of values and arithmetic operators.

Arithmetic expansion only supports integers (whole numbers, no decimals), but can perform quite a number of different operations. Here are a few of the supported operators:

# Table 7-1: Arithmetic Operators

| Operator | Description |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division (but remember, since expansion only supports integer arithmetic, results are integers.) |
| % | Modulo, which simply means, “ remainder.” |
| ** | Exponentiation |

Spaces are not significant in arithmetic expressions and expressions may be nested. For example, to multiply 5 squared by 3:

```
[me@linuxbox ~]$ echo $((($(5*2)) * 3))
75
```

Single parentheses may be used to group multiple subexpressions. With this technique, we can rewrite the example above and get the same result using a single expansion instead of two:
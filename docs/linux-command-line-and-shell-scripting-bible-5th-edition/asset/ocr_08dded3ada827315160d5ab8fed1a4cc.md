```
$ ./SingleParens.shecho
 $ cat: /etc/PASSWORD: No such file or directory
 The subshell command was NOT successful.
 $
```

Because the subshell command contained an incorrect filename in its operation, the exit status was not set to 0. Thus, the `else` command was triggered instead of the `then` command.

# Using double parentheses

The `double parentheses` command allows you to incorporate advanced mathematical formulas in your comparisons. The `test` command allows for only simple arithmetic operations in the comparison. The double parentheses command provides more mathematical symbols, which programmers who have used other programming languages may be familiar with using. Here's the format of the double parentheses command:

```
(( expression ))
```

The `expression` term can be any mathematical assignment or comparison expression. Besides the standard mathematical operators that the `test` command uses, the additional operators shown in Table 12.4 are available for use in the double parentheses command.

TABLE 12.4 The Double Parentheses Command Symbols

| Symbol | Description |
| :--- | :--- |
| val++ | Post-increment |
| val-- | Post-decrement |
| ++val | Pre-increment |
| --val | Pre-decrement |
| ! | Logical negation |
| ~ | Bitwise negation |
| ** | Exponentiation |
| << | Left bitwise shift |
| >> | Right bitwise shift |
| & | Bitwise Boolean AND |
| | | Bitwise Boolean OR |
| && | Logical AND |
| \|\| | Logical OR |

You can use the double parentheses command in an `if` statement, as well as in a normal command in the script for assigning values:
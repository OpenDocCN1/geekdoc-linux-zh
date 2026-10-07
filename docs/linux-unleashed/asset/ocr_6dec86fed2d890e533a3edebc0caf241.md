For example, if you want to print the string **Don't do that!** to the screen by enclosing it in single quotes, enter the following command:

```
print 'Don\'t do that!','\n';
```

# **NOTE**

> Remember that if you put a newline character into a single quoted string, it just prints `\n` and doesn't insert a newline character.

Just as is the case with numbers, Perl provides several operators that can be used to manipulate and compare strings. **Table 28.3** lists Perl's string operators.

# **TABLE 28.3.** **PERL'S STRING OPERATORS.**

| *Operator* | *Description* |
| :--- | :--- |
| `op1 . op2` | Concatenates op1 and op2 |
| `op1 x op2` | Repeats op1, op2 times |
| `op1 eq op2` | Returns True if op1 equals op2 |
| `op1 ge op2` | Returns True if op1 is greater than or equal to op2 |
| `op1 gt op2` | Returns True if op1 is greater than op2 |
| `op1 le op2` | Returns True if op1 is less than or equal to op2 |
| `op1 lt op2` | Returns True if op1 is less than op2 |
| `op1 ne op2` | Returns True if op1 is not equal to op2 |


# # File Operators

Just like the shell programming languages, Perl has a number of operators that exist only to test for certain conditions that exist in directories and files. The most useful of these operators are listed in **Table 28.4**.

# **TABLE 28.4.** **PERL FILE OPERATORS.**

| *Operator* | *Description* |
| :--- | :--- |
| `-B` | File is a binary file |
| `-d` | File is a directory |

*continues*
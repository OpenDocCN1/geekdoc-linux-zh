# ACTION

Just as expr is a powerful program for solving arithmetic expressions, performing operations on strings, the test command can be used to perform comparisons. test will perform comparisons on strings, as well as numeric values. Always, test will return 1 if the condition is true and 0 if it is false. It is standard for UNIX shells to use these values as true and false.

There are three types of operations for which test is used. There are numeric comparisons, string comparisons, and status tests for the file system. First up are the numeric comparisons.

Because the shell treats the less-than and greater-than symbols as redirection characters, it can't be used within the test command. Instead, I have a series of two-letter flags, as described in Table 16.1. These flags are always placed between the two arguments:

```
test -eq 4
```

This example would return false because 3 and 4 are not equal.

# Table 16.1. Test operators.

| Flag | Meaning |
| - | - |
| -eq | True if the numbers are equal |
| -ne | True if the numbers are not equal |
| -lt | True if the first number is less than the second number |
| -le | True if the first number is less than or equal to the second number |
| -gt | True if the first number is greater than the second number |
| -ge | True if the first number is greater than or equal to the second number |

You can use expr, or any other command that returns a numeric value, in test. There is also a special expression in test, -l string, which returns the length of a string. You, you can write the following tests:

```
test `expr $value % 10` -eq -l $string
test `wc -l $filename` -ge 10000
```

The first test determines if the last digit of $value (the remainder of division by 10) is the same as the length of $string. The second takes a count of the number of lines in a file and is true if there are 10,000 lines or more present.
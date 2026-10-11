**Table 27-6** bash builtins (continued)

| Builtin | Function |
| --- | --- |
| read | Reads a line from standard input (page 937) |
| readonly | Declares a variable to be readonly (page 303) |
| set | Sets shell flags or command-line argument variables; with no argument, lists all variables (pages 339 and 934) |
| shift | Promotes each command-line argument (page 933) |
| test | Compares arguments (page 889) |
| times | Displays total times for the current shell and its children |
| trap | Traps a signal (page 943) |
| type | Displays how each argument would be interpreted as a command (page 937) |
| umask | Returns the value of the file-creation mask (page 440) |
| unset | Removes a variable or function (page 303) |
| wait | Waits for a background process to terminate |

# EXPRESSIONS

An expression is composed of constants, variables, and operators that can be processed to return a value. This section covers arithmetic, logical, and conditional expressions as well as operators. Table 27-8 on page 953 lists the `bash` operators.

# ARITHMETIC EVALUATION

The Bourne Again Shell can perform arithmetic assignments and evaluate many different types of arithmetic expressions, all using integers. The shell performs arithmetic assignments in a number of ways. One is with arguments to the `let` builtin:

```
`$ let "VALUE=VALUE + 10 + NEW"`
```

In the preceding example, the variables `VALUE` and `NEW` contain integer values. Within a `let` statement you do not need to use dollar signs ($) in front of variable names. Double quotation marks must enclose a single argument, or expression, that contains SPACES. Because most expressions contain SPACES and need to be quoted, `bash` accepts `((expression))` as a synonym for `let "expression"`, obviating the need for both quotation marks and dollar signs:

```
`$ ((VALUE=VALUE + 10 + NEW))`
```

You can use either form wherever a command is allowed and can remove the SPACES if you like. In the following example, the asterisk (*) does not need to be quoted because the shell does not perform pathname expansion on the right side of an assignment (page 302):

```
`$ let VALUE=VALUE*10+NEW`
```
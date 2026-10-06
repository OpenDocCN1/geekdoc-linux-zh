# $(...) Command Substitution

Command substitution (page 575) allows you to use standard output of a command-line-in within a shell script. (Another way of using standard output is to send it to a file and read it in.) Command substitution is another type of command line expansion that occurs after the tokens on the command line have been identified. The preferred syntax for command substitution is

```
$$(command)
```

This notation instructs the shell to replace the token with standard output of command. To use standard output of command, the shell must first run command successfully. The TC Shell supports the `command` format of command substitution only.

# Arithmetic Expansion

The shell performs arithmetic expansion by evaluating an arithmetic expression and replacing it with the result. Arithmetic expansion is different for each of the three shells. Refer to “Numeric Variables” on page 701 and “Arithmetic Expansion” on page 804. Under bash syntax for arithmetic expansion is

```
$$(expression)
```

The rules for forming an expression are the same as those found in the C programming language; all standard C arithmetic operators are available. Arithmetic in bash is done using integers, although often the shell must convert string-valued variables to integers for the purpose of arithmetic evaluation.

The following example uses arithmetic expansion and command substitution to estimate the number of pages required to print the contents of file letter.txt. The dollar sign and parentheses instruct the shell to perform command substitution; the dollar sign and brackets indicate arithmetic expansion.

```
$$ echo $$(wc -l letter.txt | cut -c1-7)/66 + 1
```

The output of the wc utility with the -l option is the number of lines in the file, columns 1 through 7, followed by a SPACE and the name of the file (the first command in the following example). The cut utility with the -c option extracts the first seven columns (the second command). Arithmetic expansion is then used to divide this count by 66, the number of lines in a page. A 1 is added at the end because the integer division results in any remainder being discarded (preceding example):

```
$$ wc -l letter.txt
351 letter.txt
```

![](bbox=[0.055, 0.935, 0.075, 0.955])
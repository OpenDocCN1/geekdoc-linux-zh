
## Table 10.2 Shortcut Operators

| Operator | Example | Equivalent To |
|---|---|---|
| += | @ num += 2 | @ num = $num + 2 |
| -= | @ num -= 4 | @ num = $num - 4 |
| *= | @ num *= 3 | @ num = $num * 3 |
| /= | @ num /= 2 | @ num = $num / 2 |
| ++ | @ num++ | @ num = $num + 1 |
| -- | @ num-- | @ num = $num - 1 |

### EXAMPLE 10.5

```
1
% @ sum = 4 + 6
echo $sum
10

2
% @ sum++
echo $sum
11

3
% @ sum += 3
echo $sum
14

4
% @ sum--
echo $sum
13

5
% @ n = 3+4
@: Badly formed number
```

### EXPLANATION

+   1. The variable sum is assigned the result of adding 4 and 6. (The space after the @ is required.)
+   2. The variable sum is incremented by 1.
+   3. The variable sum is incremented by 3.
+   4. The variable sum is decremented by 1.
+   5. Spaces are required after the @ symbol and surrounding the operator.

## 10.3.2 Floating-Point Arithmetic

Because floating-point arithmetic is not supported by this shell, if you should need more complex mathematical operations, you can use UNIX utilities.

The bc and awk utilities are useful if you need to perform complex calculations.

### EXAMPLE 10.6

(The Command Line)

```
1 set n=`echo "scale=3; 13 / 2" | bc`
echo $n
6.500
```

```
2 set product=`nawk -v x=2.45 -v y=3.124 'BEGIN{\nprintf "%.2f\n", x + y }'`
% echo $product
7.65
```

### EXPLANATION

1 The output of the echo command is piped to the bc program. The scale is set to 3; that is, the number of significant digits to the right of the decimal point that will be printed. The calculation is to divide 13 by 2. The entire pipeline is enclosed in backquotes. Command substitution will be performed and the output assigned to the variable n.

2 The awk program gets its values from the argument list passed in at the command line. Each argument passed to awk is preceded by the -v switch; for example, -v x=2.45 and -v y=3.124. After the numbers are multiplied, the printf function formats and prints the result with a precision of 2 places to the right of the decimal point. The output is assigned to the variable product.

## 10.4 Debugging Scripts

C/TC shell scripts often fail because of some simple syntax error or logic error. Options to the csh command to help you debug your programs are provided in Table 10.3.

## Table 10.3 echo (-x) and verbose (-v)

| Option | What It Does |
|---|---|
| As Options to csh and tcsh | |
| csh -x scriptname
tcsh -x scriptname | Display each line of script after variable substitution and before execution. |
| csh -v scriptname
tcsh -v scriptname | Display each line of script before execution, just as you typed it. |
| csh -n scriptname
tcsh -n scriptname | Interpret but do not execute commands. |
| As Arguments to the set Command | |
| set echo | Display each line of script after variable substitution and before execution. |
| set verbose | Display each line of script before execution, just as you typed it. |

### Table 10.3 echo (-x) and verbose (-v) (continued)

| Option | What It Does |
|---|---|
| As the First Line in a Script | |
| #!/bin/csh -xv | Turns on both echo and verbose. These options can be invoked separately or |
| #!/bin/tcsh -xv | combined with other csh invocation arguments. |

### EXAMPLE 10.7

(The -v and -x Options)

```
1
% cat practice
#!/bin/csh
echo Hello $LOGNAME
echo The date is `date`
echo Your home shell is $SHELL
echo Good-bye $LOGNAME
```

```
2
% csh -v practice
echo Hello $LOGNAME
Hello ellie
echo The date is `date`
The date is Sun May 23 12:24:97 PDT 2004
echo Your login shell is $SHELL
Your login shell is /bin/csh
echo Good-bye $LOGNAME
Good-bye ellie
```

```
3
% csh -x practice
echo Hello ellie
Hello ellie
echo The date is `date`
date
The date is Sun May 23 12:24:15 PDT 2004
echo Your login shell is /bin/csh
Your login shell is /bin/csh
echo Good-bye ellie
Good-bye ellie
```

### EXPLANATION

+   1 The contents of the C shell script are displayed. Variable and command substitution lines are included so that you can see how echo and verbose differ.
+   2 The -v option to the csh command causes the verbose feature to be enabled. Each line of the script is displayed as it was typed in the script, and then the line is executed.
+   3 The -x option to the csh command enables echoing. Each line of the script is displayed after variable and command substitution are performed, and then the line is executed. Because this feature lets you examine what is being replaced as a result of command and variable substitution, it is used more often than the verbose option.


+   d. Display whether a file is a simple file or a directory
+   e. Create a backup for a file
+   f. Start a telnet session
+   g. Start an ftp session
+   h. Exit

Option (c) requires that you ask the user for a list of login names. For options (d) and (e), prompt the user for file names before invoking a shell command/program. For options (f) and (g), prompt the user for a domain name (or IP address) before initiating a telnet or ftp session. The program should allow the user to try any option any number of times and should quit only when the user gives option (h) as input. A good programming practice is to build code incrementally—that is, write code for one option, test it, and then go to the next option. Use this style of code development for writing this shell script.

## 19. Write a shell script that reads a string from the keyboard. If the string is a pathname for a directory in your system's directory structure, the script displays the counts of all types of files in it in the following format:

+   Directories :
+   Block special files :
+   Character special files :
+   Link files :
+   FIFOs :
+   Ordinary files :
+   Sockets :

The script displays the cumulative size (in bytes) for all ordinary files in the directory. Do the appropriate exception handling.

## Advanced C Shell Programming

## Objectives

- To discuss numeric data processing
- To describe array processing
- To discuss how standard input of a command in a shell script can be redirected to data within the script
- To explain signal/interrupt processing capability of the C shell
- To cover the commands and primitives
  `=, +=, -=, *=, /=, %=, ==, <=, >=, |, &, (), <<, @, <^Z>, <^C>, clear, kill, onintr, set, stty`

### 15.1 INTRODUCTION

We did not discuss four features of C shell programming in Chapter 14: processing of numeric data, array processing, the here document, and interrupt processing. In this chapter, we discuss these features and give some example scripts that use them. We also describe how C shell scripts can be debugged.

### 15.2 NUMERIC DATA PROCESSING

The C shell has a built-in capability for processing numeric data. It allows you to perform arithmetic and logic operations on numeric integer data without explicitly converting string data to numeric data and vice versa. You can use the @ command to declare numeric variables, the variables that contain integer data. This command allows declaration of local variables only. The following is a brief description of the command.

## SYNTAX

```
@ variable [operator expression] [variable [operator expression]] ...
```

Purpose: To declare variable to be a numeric variable, evaluate the arithmetic expression, apply the operator specified in operator to the current value of variable and the value of expression, and assign the result to variable

Expressions are formed by using the arithmetic and logic operators summarized previously in Table 14.4. Although octal numbers can be used in expressions by starting them with 0, the final value of an arithmetic expression is always expressed in decimal numbers. The elements of an expression must be separated by one or more spaces unless the elements are (, ), &, |, <, and >. Table 15.1 describes the possible assignment operators that can be used.

In the following interactive session, the numeric variables value1 and value2 are initialized to 10 and 15, respectively. The echo command is used to show that the assignments work properly.

```
% @ value1=10
% @ value2=15
% echo "$value1 $value2"
10 15
%
```

In the following session, the @ command declares two variables, difference and sum, and initializes them to the values of the expressions to the right of the respective = signs. These actions result in the variables difference and sum taking the values −5 and 25, respectively.

```
% @ difference = ( $value1 - $value2 ) sum = ( $value1 + $value2 )
% echo "$difference $sum"
-5 25
%
```

## TABLE 15.1 Assignment Operators for the @ Command

| Operator | Meaning |
|---|---|
| = | Assigns the value of the expression on the right-hand side of = to the variable preceding it |
| += | Adds the value of the expression on the right-hand side of = to the current value of the variable preceding it and assigns the result to the variable |
| -= | Subtracts the value of the expression on the right-hand side of = from the current value of the variable preceding it and assigns the result to the variable |
| *= | Multiplies the value of the expression on the right-hand side of = by the current value of the variable preceding it and assigns the result (product) to the variable |
| /= | Divides the value of the variable preceding = by the value of the expression on the right-hand side of = and assigns the result (quotient) to the variable |
| %= | Divides the value of the variable preceding = by the value of the expression on the right-hand side of = and assigns the remainder to the variable |

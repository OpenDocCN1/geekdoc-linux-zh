# EXPLANATION (CONTINUED)

+   6 The user is asked to press Enter when ready.
+   7 Whatever the user types is read into the variable JUNK, and when Enter is pressed, the program will resume execution.
+   8 The lpd program starts the print daemon.

# 14.3 Arithmetic

# 14.3.1 Integers (declare and let Commands)

# The declare Command.

Variables can be declared as integers with the declare -i command. If you attempt to assign any string value, bash assigns 0 to the variable. Arithmetic can be performed on variables that have been declared as integers. (If the variable has not been declared as an integer, the built-in let command allows arithmetic operations. See "The let Command" on page 873.) If you attempt to assign a floating-point number, bash reports a syntax error. Numbers can also be represented in different bases such as binary, octal, and hex.

# EXAMPLE 14.6

```
1 $ declare -i num
2 $ num=hello
$ echo $num
0
3 $ num=5 + 5
bash: +: command not found
4 $ num=3+5
$ echo $num
10
5 $ num=4*6
$ echo $num
24
6 $ num="4 + 6"
$ echo $num
24
7 $ num=6.5
bash: num: 6:5: syntax error in expression (remainder of expression is ".5")
```

# EXPLANATION

+   1 The declare command with the -i option creates an integer variable num.
+   2 Trying to assign the string hello to the integer variable num causes the string to be stored as 0.
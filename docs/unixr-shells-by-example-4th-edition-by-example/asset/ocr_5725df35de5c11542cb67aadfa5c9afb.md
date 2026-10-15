# EXPLANATION

+   1 The declare function is used to assign an integer variable x the octal value 017. Octal numbers must start with a leading 0. 15, the decimal value of 017, is printed.
+   2 The variable x is assigned the value 101 (binary). 2 represents the base, separated by a #, and the number in that base, 101. The value of x is printed as decimal, 5.
+   3 The variable x is assigned the value 17 (octal). The value of x is printed as decimal, 15.
+   4 The variable x is assigned the value b (hexadecimal). The value of x is decimal 11.

# The let Command.

The let command is a bash built-in command that is used to perform integer arithmetic and numeric expression testing. To see what let operators your version of bash supports, type at the prompt:

```
help let
```

A list of the let operators is also found in Table 14.4 on page 884.

# EXAMPLE 14.9

(The Command Line)

```
1 $ i=5 or let i=5
$ let i=i+1
$ echo $i
6
3 $ let "i = i + 2"
$ echo $i
8
4 $ let "i+=1"
$ echo $i
9
5 $ i=3
6 $ (( i+=4 ))
$ echo $i
7
7 $ (( i-=2 ))
$ echo $i
5
```

# EXPLANATION

+   1 The variable i is assigned the value 5.
+   2 The let command will add 1 to the value of i. The $ (dollar sign) is not required for variable substitution when performing arithmetic.
+   3 The quotes are needed if the arguments contain whitespace.
+   4 The shortcut operator, +=, is used to add 1 to the value of i.
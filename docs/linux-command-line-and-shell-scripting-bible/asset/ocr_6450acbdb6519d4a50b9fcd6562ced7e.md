# The Korn Shell

Probably the most useful feature of the ksh93 shell's mathematical abilities is that unlike the bash
shell, it can handle floating point numbers:

```
$ let value=\ 10.5 * 0.5"
$ echo $value
5.25
$
```

This feature alone makes the ksh93 shell a favorite for many shell programmers.

Instead the let command, you can also use the double parentheses method of defining math-
emical operations:

```
$ value1=$(( 4 * 3 ))
$ echo $value1
12
$
```

You can perform any mathematical operation you need within the double parentheses, using both
numbers and variables:

```
$ value1=10.25
$ value2=$(( $value / 10 ))
$ echo $value2
1.025
$
```

If you try to perform something that's not valid, the ksh93 shell will let you know about it
an error message:

```
$ value1=0
$ value2=$(( 10.25 / $value ))
k93: 10.25 / 0 : divide by zero
$
```

Besides the error message, the ksh93 shell also returns a non-zero exit status to indicate that the
operation failed.

# Mathematical functions

The ksh93 shell includes several built-in mathematical functions you can use in your shell scripts.
The mathematical library built into the ksh93 consists of the following functions:

+   - abs(x): Absolute value of x.
- acos(x): The arc cosine of x (in radians).
- asin(x): The arc sine of x (in radians).
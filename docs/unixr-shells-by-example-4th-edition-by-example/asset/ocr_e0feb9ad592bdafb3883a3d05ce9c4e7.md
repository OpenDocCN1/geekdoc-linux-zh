When using the escape sequences, don't forget to use the -e switch!

# EXAMPLE 13.57

```
1  $ echo The username is $LOGNAME.
    The username is ellie.

2  $ echo -e "\t\tHello there\c"
    Hello there$

3  $ echo -n "Hello there"
    Hello there$
```

# EXPLANATION

+   1 The echo command prints its arguments to the screen. Variable substitution is performed by the shell before the echo command is executed.
+   2 The echo command, with the -e option, supports escape sequences similar to those of the C programming language. The $ is the shell prompt.
+   3 When the -n option is on, the line is printed without the newline. The escape sequences are not supported by this version of echo.

# The printf Command.

The GNU version of printf¹¹ can be used to format printed output. It prints the formatted string in the same way as the C printf function. The format consists of a string that may contain formatting instructions to describe how the printed output will look. The formatting instructions are designated with a % followed by specifiers (d i o u x X f e g G s) where %f would represent a floating-point number and %d would represent a whole (decimal) number.
To see a complete listing of printf specifiers and how to use them, type printf --help at the command-line prompt. To see what version of printf you are using, type printf --version. If you are using bash 2.x, the built-in printf command uses the same format as the executable version in /usr/bin.

# FORMAT

```
printf format [argument...]
```

# EXAMPLE 13.58

```
printf "%10.2f\n" 10.5 25
```
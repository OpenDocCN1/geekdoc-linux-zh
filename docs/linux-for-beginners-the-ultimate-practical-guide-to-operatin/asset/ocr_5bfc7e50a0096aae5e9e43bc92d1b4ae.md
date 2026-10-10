> Note: The 2 * 2 expression returns a syntax error. We have to use an escape character to resolve the problem.

Rather than using the expr command, it is more convenient to use brackets.

```
#!/bin/bash
var1=2
var2=6
var3=3
var4=$(expr $var1 \* $var2)
echo $var4
var5=[ $(($var1 * $var2))/$var3]
echo $var5
```

```
jan@jan-virtual-machine:~/Desktop$ ./Myscript
12
4
```

# The Bash Calculator

When you want to perform more complex mathematical functions, there is a built-in bash tool to perform this. It is the bash calculator. The command is bc.

```
jan@jan-virtual-machine:~/Desktop$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
quit
```

> Tip: To exit from this tool, type quit and press enter. While in bc, you can perform math operations.

The bash calculator supports the following.

+   - Numerical values (integer and floating-point numbers).
+   - Variables.
+   - Expressions.
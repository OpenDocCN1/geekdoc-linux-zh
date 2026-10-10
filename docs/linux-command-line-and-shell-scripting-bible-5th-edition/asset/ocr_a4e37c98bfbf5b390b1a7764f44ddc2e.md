Running this script produces the following output:

```
$ chmod u+x test7
$ ./test7
The final result is 500
$
```

Also, notice that when using the square brackets method for calculating equations you don't need to worry about the multiplication symbol, or any other characters, being misinterpreted by the shell. The shell knows that it's not a wildcard character because it is within the square brackets.

There's one major limitation to performing math in the Bash shell script. Take a look at this example:

```
$ cat test8
#!/bin/bash
var1=100
var2=45
var3=$[var1 / $var2]
echo The final result is $var3
$
```

Now run it and see what happens:

```
$ chmod u+x test8
$ ./test8
The final result is 2
$
```

The Bash shell mathematical operators support only integer arithmetic. This is a huge limitation if you're trying to do any sort of real-world mathematical calculations.

> **Note**
> The *z* shell (*zsh*) provides full floating-point arithmetic operations. If you require floating-point calculations in your shell scripts, you might consider checking out the *z* shell (discussed in Chapter 23, "The *zsh* Shell").

# A floating-point solution

There are several solutions for overcoming the Bash integer limitation. The most popular solution uses the built-in Bash calculator, called *bc*.

# The basics of *bc*

The Bash calculator is actually a programming language that allows you to enter floating-point expressions at a command line and then interprets the expressions, calculates them, and returns the result. The Bash calculator recognizes the following:

+   □ Numbers (both integer and floating point)
+   □ Variables (both simple variables and arrays)
+   □ Comments (lines starting with a pound sign or the C language / * * / pair)
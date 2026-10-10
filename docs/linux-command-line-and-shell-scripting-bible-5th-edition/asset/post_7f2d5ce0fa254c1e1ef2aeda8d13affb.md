
# Part II: Shell Scripting Basics

This command sequence runs the **rpm** command, pipes the output to the **sort** command, and then pipes that output to the **more** command to display the data, stopping after every screen of information. This now lets you pause and read what's on the display before continuing, as shown in Figure 11.1.

### FIGURE 11.1
Using piping to send data to the more command.

![](img/0798d50a0e5dbf1265fbda3832b3e015_279_0.png)

To get even fancier, you can use redirection along with piping to save your output to a file:

```
$ rpm -qa | sort > rpm.list
$ more rpm.list

aajohan-comfortaa-fonts-3.001-10.el9.noarch
aarvarr-dns-1.12.2-1.el9_5.x86_64
abattis-cantarell-fonts-0.301-4.el9.noarch
accountserviced-0.6.55-10.el9.x86_64
accountsservice-liba-0.6.55-10.el9.x86_64
acl-2.3.1-4.el9.x86_64
adcl1-0.9.2-1.el9.x86_64
adobe-mappings-cmap-20171205-12.el9.noarch
adobe-mappings-cmap-deprecated-20171205-12.el9.noarch
adobe-mappings-pdf-20180407-10.el9.noarch
adobe-source-code-pro-fonts-2.030.1.050-12.el9_1.noarch
adwaita-cursor-theme-40.1.1-3.el9.noarch
adwaita-gtk2-theme-3.28-14.el9.x86_64
adwaita-icon-theme-40.1.1-3.el9.noarch
```

As expected, the data in the `rpm.list` file is now sorted!

By far, one of the most popular uses is piping the results of commands that produce long output to the `more` command. This is especially common with the `ls` command, as shown in Figure 11.2.

![](img/0798d50a0e5dbf1265fbda3832b3e015_280_0.png)

The `ls -l` command produces a long listing of all the files in the directory. For directories with lots of files, this can be quite a listing. By piping the output to the `more` command, you force the output to stop at the end of every screen of data.

## Performing Math

Another feature crucial to any programming language is the ability to manipulate numbers. Unfortunately, for shell scripts this process is a bit awkward. You have two ways to perform mathematical operations in your shell scripts.

### Using the `expr` command

Originally, the Bourne shell provided a special command that was used for processing mathematical equations. The `expr` command allowed the processing of equations from the command line, but it is extremely clunky:

```
$ expr 1 + 5
6
```

The `expr` command recognizes a few different mathematical and string operators, shown in Table 11.1.

### TABLE 11.1 The `expr` Command Operators

| Operator | Description |
| :--- | :--- |
| `ARG1 \| ARG2` | Returns `ARG1` if either argument is null or 0; otherwise, returns `ARG2` |
| `ARG1 & ARG2` | Returns `ARG1` if neither argument is null or 0; otherwise, returns 0 |
| `ARG1 < ARG2` | Returns 1 if `ARG1` is less than `ARG2`; otherwise, returns 0 |
| `ARG1 <= ARG2` | Returns 1 if `ARG1` is less than or equal to `ARG2`; otherwise, returns 0 |
| `ARG1 = ARG2` | Returns 1 if `ARG1` is equal to `ARG2`; otherwise, returns 0 |
| `ARG1 != ARG2` | Returns 1 if `ARG1` is not equal to `ARG2`; otherwise, returns 0 |
| `ARG1 >= ARG2` | Returns 1 if `ARG1` is greater than or equal to `ARG2`; otherwise, returns 0 |
| `ARG1 > ARG2` | Returns 1 if `ARG1` is greater than `ARG2`; otherwise, returns 0 |
| `ARG1 + ARG2` | Returns the arithmetic sum of `ARG1` and `ARG2` |
| `ARG1 - ARG2` | Returns the arithmetic difference of `ARG1` and `ARG2` |
| `ARG1 * ARG2` | Returns the arithmetic product of `ARG1` and `ARG2` |
| `ARG1 / ARG2` | Returns the arithmetic quotient of `ARG1` divided by `ARG2` |
| `ARG1 % ARG2` | Returns the arithmetic remainder of `ARG1` divided by `ARG2` |
| `STRING : REGEXP` | Returns the pattern match if REGEXP matches a pattern in `STRING` |
| `match STRING REGEXP` | Returns the pattern match if REGEXP matches a pattern in `STRING` |
| `substr STRING POS LENGTH` | Returns the substring LENGTH characters in length, starting at position `POS` (starting at 1) |
| `index STRING CHARS` | Returns position in `STRING` where `CHARS` is found; otherwise, return 0 |
| `length STRING` | Returns the numeric length of the string `STRING` |
| `+ TOKEN` | Interprets `TOKEN` as a string, even if it’s a keyword |
| `(EXPRESSION)` | Returns the value of `EXPRESSION` |

The standard operators work fine in the `expr` command, but the problem occurs when using them from a script or the command line. Many of the `expr` command operators have other meanings in the shell (such as the asterisk). Using them in the `expr` command produces odd results:

```
$ expr 5 * 2
expr: syntax error
$
```

To solve this problem, you need to use the shell escape character (the backslash) to identify any characters that may be misinterpreted by the shell before being passed to the `expr` command:

```
$ expr 5 \* 2
10
$
```

Now that’s really starting to get ugly! Using the `expr` command in a shell script is equally cumbersome:

```
$ cat test6
#!/bin/bash
# An example of using the expr command
var1=10
var2=20
var3=$(expr $var2 / $var1)
echo The result is $var3
```

To assign the result of a mathematical equation to a variable, you have to use command substitution to extract the output from the `expr` command:

```
$ chmod u+x test6
$ ./test6
The result is 2
$
```

Fortunately, the Bash shell has an improvement for processing mathematical operators, as you learn in the next section.

### Using brackets

The Bash shell includes the `expr` command to stay compatible with the Bourne shell; however, it also provides a much easier way of performing mathematical equations. In Bash, when assigning a mathematical value to a variable, you can enclose the mathematical equation using a dollar sign and square brackets (`$[ operation]`):

```
$ var1=$[1 + 5]
$ echo $var1
6
$ var2=$[$var1 * 2]
$ echo $var2
12
$
```

Using brackets makes shell math much easier than with the `expr` command. The same technique also works in shell scripts:

```
$ cat test7
#!/bin/bash
var1=100
var2=50
var3=45
var4=$[$var1 + ($var2 - $var3)]
echo The final result is $var4
$
```

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

## A floating-point solution

There are several solutions for overcoming the Bash integer limitation. The most popular solution uses the built-in Bash calculator, called *bc*.

### The basics of *bc*

The Bash calculator is actually a programming language that allows you to enter floating-point expressions at a command line and then interprets the expressions, calculates them, and returns the result. The Bash calculator recognizes the following:

- Numbers (both integer and floating point)
- Variables (both simple variables and arrays)
- Comments (lines starting with a pound sign or the C language `/* */` pair)
- Expressions
- Programming statements (such as if-then statements)
- Functions

You can access the Bash calculator from the shell prompt using the `bc` command:

```
$ bc
bc 1.07.1
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006, 2008, 2012-2017 Free
Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type 'warranty'.
12 * 5.4
64.8
3.156 * (3 + 5)
25.248
quit
$
```

The example starts out by entering the expression `12 * 5.4`. The Bash calculator returns the answer. Each subsequent expression entered into the calculator is evaluated, and the result is displayed. To exit the Bash calculator, you must enter `quit`.

The floating-point arithmetic is controlled by a built-in variable called `scale`. You must set this value to the desired number of decimal places you want in your answers or you won't get what you were looking for:

```
$ bc -q
3.44 / 5
0
scale=4
3.44 / 5
.6880
quit
$
```

The default value for the `scale` variable is 0. Before the `scale` value is set, the Bash calculator provides the answer to zero decimal places. After you set the `scale` variable value to 4, the Bash calculator displays the answer to four decimal places. The `-q` command-line parameter suppresses the lengthy welcome banner from the Bash calculator.

In addition to normal numbers, the Bash calculator understands variables:

```
$ bc -q
var1=10
var1 * 4
40
var2 = var1 / 5
print var2
2
quit
$
```

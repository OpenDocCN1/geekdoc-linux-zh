
⇒ Here are some ways to use this.

+   - To output the result of 50 times 10, type:

```
$ calc 50*10 RET
500
$
```

+   - To output the result of 100 times the sum of 4 plus 420, type:

```
$ calc '100*(4+420)' RET
42400
$
```

+   - To output the remainder of 10 divided by 3, type:

```
$ calc 10%3 RET
1
$
```

**NOTES:** This is a method for speed. It’s useful for quickly computing a simple arithmetic equation at the shell prompt, but it has several drawbacks: It only outputs whole integers; its operators are limited; and complex expressions must be quoted. Still, if you’re at a shell prompt and need to know the product of 12,342 and 587, I don’t think there’s a faster way. But for doing anything more than the very simplest operations, see the next recipe, which describes bc.

## 29.1.2 Using a Calculator

bc
DEB: bc
RPM: bc
WWW: http://www.gnu.org/software/bc/

There are a great many calculators, for X or any terminal. One of the more venerable standbys is bc, a calculation language that supports arbitrary-precision numbers, scripts, variables, functions, and algebraic statements. Use it when you have a lot of calculations to make, or when you must compute numbers with decimals.

Type bc to start it; you can then perform arithmetic operations interactively, just as you would with a desktop calculator or adding machine.

When you are running bc, you type each statement to be evaluated on a line by itself, typing [RET] at the end of the statement; the evaluation of what you type is output on the following line. Each line you type will be evaluated by bc as an arithmetic expression. To exit, type quit on a line by itself.

⇒ To multiply 42 by 17 with bc, type:

```
$ bc [RET]
bc 1.06
Copyright 1991, 1992, 1993, 1994, 1997, 1998, 2000 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type 'warranty'.
42 * 17 [RET]
714
quit [RET]
$
```

In this example, bc output its version number and warranty information when it started; then, the statement “42 * 17” was typed by the user, bc output the result (“714”), and then the user typed quit to exit bc.

By default, digits to the right of the decimal point are truncated from the output—so dividing 10 by 3 would output “3” as a result, and outputting the remainder from this operation by typing “10%3” would output “1.” But since bc is an arbitrary-precision calculator, you can give the number of digits to use after the decimal point. Do this by specifying the value of the scale variable; its default value is 0.

⇒ To use bc to compute the result of 10 divided by 3, using 20 digits after the decimal point, type:

```
$ bc [RET]
bc 1.06
Copyright 1991, 1992, 1993, 1994, 1997, 1998, 2000 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type 'warranty'.
scale=20 [RET]
10 / 3 [RET]
3.333333333333333333
quit [RET]
$
```

Use the -l option to start bc with a scale of 20, and with a number of math functions loaded, as described in the following table.

|  |  |
|---|---|
| s (x) | Outputs sine of x (x is given in radians). |
| c (x) | Outputs cosine of x (x is given in radians). |
| a (x) | Outputs arctangent of x, in radians. |
| l (x) | Outputs the logarithm of x. |
| e (x) | Outputs the exponential function of e to the xth power. |
| j (n,x) | Outputs the Bessel function of integer order n of x. |

The following table describes the symbols you can use to specify mathematical operations.

|  |  |
|---|---|
| expression + expression | Add: Output the sum of the two expressions. |
| expression - expression | Subtract: Output the difference of the two expressions. |
| expression * expression | Multiply: Output the product of the two expressions. |
| expression / expression | Divide: Output the quotient of the two expressions. |

expression % expression
Remainder: Output the remainder resulting from dividing the two expressions.

expression ^ expression
Power: Raise the first expression to the power of the second expression.

(expressions)
Group an expression or expressions together, altering the standard precedence of performing operations.

sqrt(expression)
Output the square root of expression.

The -q option is nice—it suppresses the copyright and warranty message at start-up. Starting bc with both this and the -l option is a good way to run it, and you might want to make an alias for bc with these two options (see Recipe 3.6 [Using Alias Words], page 82):

```
alias bc='/usr/bin/bc -ql'
```

## 29.2 Outputting a Random Number

To get a random number, display the contents of the RANDOM variable. It is a special shell variable that outputs a random integer between 0 and 32,767.

⇒ To output a random number, type:

```
$ echo $RANDOM [RET]
```

To output a random number in a range starting from zero but under a certain number, use RANDOM with the Bash arithmetic evaluation expression "$(($RANDOM % number))," where number is the integer that the output should be under.

⇒ To output a random number from 0 to 9, type:

```
$ echo $(($RANDOM % 10)) [RET]
```

## 29.3 Listing a Sequence of Numbers

Use seq to print a sequence of numbers. This is very useful for getting a listing of numbers to use as arguments, or for otherwise passing sequences of numbers to commands.

To output the sequence from 1 to any number, give that number as an argument.

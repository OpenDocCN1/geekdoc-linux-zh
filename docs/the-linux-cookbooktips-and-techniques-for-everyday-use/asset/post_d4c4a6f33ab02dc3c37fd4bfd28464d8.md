
714
quit RET
$

In this example, bc output its version number and warranty information when it started; then, the statement 42 * 17 was typed by the user, bc output the result ( `714` ), and then the user typed quit to exit bc.

By default, digits to the right of the decimal point are truncated from the output—so dividing 10 by 3 would output `3` as a result, and outputting the remainder from this operation by typing 10%3 would output a `1`. However, bc is an arbitrary precision calculator, and you can give the number of digits to use after the decimal point by specifying the value of the scale variable; its default value is 0.

- To use bc to compute the result of 10 divided by 3, using 20 digits after the decimal point, type:

```
$ bc RET
bc 1.05
Copyright 1991, 1992, 1993, 1994, 1997, 1998 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
scale=20 RET
10 / 3 RET
3.333333333333333333
quit RET
$
```

The following table describes the symbols you can use to specify mathematical operations.

| SYMBOL | OPERATION |
|---|---|
| expression + expression | Add: output the sum of the two expressions. |
| expression - expression | Subtract: output the difference of the two expressions. |
| expression * expression | Multiply: output the product of the two expressions. |
| expression / expression | Divide: output the quotient of the two expressions. |
| expression % expression | Remainder: output the remainder resulting by dividing the two expressions. |
| expression ^ expression | Power: raise the first expression to the power of the second expression. |
| (expressions) | Group an expression or expressions together, altering the standard precedence of performing operations. |
| sqrt(expression) | Output the square root of expression. |

## 29.2 Outputting a Random Number

@sf (WWW): http://dsl.org/comp/tinvutils/

To output a random number, use random. Give as an argument an integer denoting the range of numbers to be output; random then outputs a random number from 0 to the number you give, minus one.

- To output a random number from 0 to 9, type:

```
$ random 10 RET
```

## 29.3 Listing a Sequence of Numbers

Use seq to print a sequence of numbers. This is very useful for getting a listing of numbers to use as arguments, or otherwise passing sequences of numbers to other commands.

To output the sequence from 1 to any number, give that number as an argument.

- To output the sequence of numbers from one to seven, type:

```
$ seq 7 RET
```

- To output the sequence of numbers from one to negative seven, type:

```
$ seq -7 RET
```

To output the sequence from any one number to another, give those numbers as arguments.

- To output the sequence of numbers from nine to zero, type:

```
$ seq 9 0 RET
```

- To output the sequence of numbers from negative one to negative twenty, type:

```
$ seq -1 -20 RET
```

To specify an increment other than one, give it as the second argument, between the starting and ending number.

- To output the sequence of numbers from -1 to 14, incrementing by 3, type:

```
$ seq -1 3 14 RET
```

Use the `-w` option to pad numbers with leading zeros so that they're all output with the same width.

Specify a separator string to be output between numbers as an argument to the `-s` option; the default is a newline character, which outputs each number in the sequence on its own line.

- To output the sequence of numbers from 9 to 999, incrementing by 23, with numbers padded with zeros so that they're all of equal width, type:

```
$ seq -w 9 23 999 RET
```

- To output the sequence of numbers from 1 to 23, with a space character between each, type:

```
$ seq -s ' ' 1 23 RET
```

To pass a sequence of numbers as arguments to a command, pipe the output of seq using a space character as a separator.

- To concatenate all the files in the current directory, whose names are numbers from 25 through 75, into a new file called `selected-mail`, type:

```
$ cat `seq -s " " 25 75` > selected-mail RET
```

## 29.4 Finding Prime Factors

The factor tool calculates and outputs the prime factors of numbers passed as arguments.

- To output the prime factors of 2000, type:

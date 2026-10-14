
This problem can be mitigated by surrounding the assignment expression with parentheses:

```
[me@linuxbox ~]$ ((a1?=(a==1):(a==1)))
```

Next, we see a more comprehensive example of using arithmetic operators in a script that produces a simple table of numbers:

```
#!/bin/bash

# arith-loop: script to demonstrate arithmetic operators

finished=0
a=0
printf "a\ta**2\ta**3\n"
printf "\t====\t====\n"
until ((finished)); do
  b=$((a**2))
  c=$((a**3))
  printf "%d\t%d\t%d\n" $a $b $c
  ((a+=1||a:(finished=1)))
done
```

In this script, we implement an until loop based on the value of the finished variable. Initially, the variable is set to 0 (arithmetic false), and we continue the loop until it becomes non-zero. Within the loop, we calculate the square and cube of the counter variable a. At the end of the loop, the value of the counter variable a is evaluated. If it is less than 10 (the maximum number of iterations), it is incremented by 1, else the variable finished is given the value of 1, making finished arithmetically true and thereby terminating the loop. Running the script gives this result:

```
[me@linuxbox ~]$ arith-loop
a	a**2	a**3
==	====	====
0	0	0
1	1	1
2	4	8
3	9	27
4	16	64
5	25	125
6	36	216
7	49	343
8	64	512
9	81	729
10	100	1000
```

## bc—An Arbitrary-Precision Calculator Language

We have seen that the shell can handle all types of integer arithmetic, but what if we need to perform higher math or even just use floating-point numbers? The answer is, we can’t. At least not directly with the shell. To do this,

we need to use an external program. There are several approaches we can take: Embedding Perl or AWK programs is one possible solution but, unfortunately, outside the scope of this book.

Another approach is to use a specialized calculator program. One such program found on most Linux systems is called bc.

The bc program reads a file written in its own C-like language and executes it. A bc script may be a separate file, or it may be read from standard input. The bc language supports quite a few features, including variables, loops, and programmer-defined functions. We won’t cover bc entirely here, just enough to get a taste. bc is well documented by its man page.

Let’s start with a simple example. We’ll write a bc script to add 2 plus 2:

```
/* A very simple bc script */

2 + 2
```

The first line of the script is a comment. bc uses the same syntax for comments as the C programming language. Comments, which may span multiple lines, begin with /* and end with */.

## Using bc

If we save the bc script above as foo.bc, we can run it this way:

```
[me@linuxbox ~]$ bc foo.bc
bc 1.06.94

Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
4
```

If we look carefully, we can see the result at the very bottom, after the copyright message. This message can be suppressed with the -q (quiet) option.

bc can also be used interactively:

```
[me@linuxbox ~]$ bc -q
2 + 2
4
quit
```

When using bc interactively, we simply type the calculations we wish to perform, and the results are immediately displayed. The bc command quit ends the interactive session.

It is also possible to pass a script to bc via standard input:

```
[me@linuxbox ~]$ bc < foo.bc
4
```

The ability to take standard input means that we can use here documents, here strings, and pipes to pass scripts. This is a here string example:

```
[me@linuxbox ~]$ bc <<< "2+2"
4
```

## An Example Script

As a real-world example, we will construct a script that performs a common calculation, monthly loan payments. In the script below, we use a here document to pass a script to bc:

```
#!/bin/bash

# loan-calc : script to calculate monthly loan payments

PROGNAME=$(basename $0)

usage () {
  cat <<- EOF
Usage: $PROGNAME PRINCIPAL INTEREST MONTHS

Where:

  PRINCIPAL is the amount of the loan.
  INTEREST is the APR as a number (7% = 0.07).
  MONTHS is the length of the loan's term.
EOF
}

if (($# != 3)); then
  usage
  exit 1
fi

principal=$1
interest=$2
months=$3

bc <<- EOF
scale = 10
i = $interest / 12
p = $principal
n = $months
a = p * ((i * ((1 + i) ^ n)) / (((1 + i) ^ n) - 1))
print a, "\n"
EOF
```

When executed, the results look like this:

```
[me@linuxbox ~]$ loan-calc 135000 0.0775 180
1270.7222490000
```

This example calculates the monthly payment for a $135,000 loan at 7.75% APR for 180 months (15 years). Notice the precision of the answer. This is determined by the value given to the special scale variable in the bc

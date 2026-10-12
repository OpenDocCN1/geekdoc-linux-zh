![](bbox=[0.0, 0.035, 0.25, 0.05])

```
T
178.99 - 326.8
-
```

After the expression has been read in, the value of o is successively compared against the values as specified by each case. When a match is found, the statements contained inside the case are executed. The b statement then sends execution out of the s statement, where execution of the program is complete. If none of the cases match the value of o , the d case, which displays U is executed.

The b statement in the d case is actually unnecessary in the preceding program because no statements follow this case inside the s . Nevertheless, it is a good programming habit to remember to include the b at the end of every case.

When writing a s statement, bear in mind that no two case values can be the same. However, you can associate more than one case value with a particular set of program statements. This is done simply by listing the multiple case values (with the keyword c before the value and the colon after the value in each case) before the common statements that are to be executed. As an example, in the following s statement, the p statement, which multiplies v by v , is executed if o is equal to an asterisk or to the lowercase letter x.

![](bbox=[0.0, 0.46, 0.25, 0.48])

```
s{



}
```

# Boolean Variables

Many new programmers soon find themselves with the task of having to write a program to generate a table of *prime numbers*. To refresh your memory, a positive integer $p$ is a prime number if it is not evenly divisible by any other integers, other than 1 and itself. The first prime integer is defined to be 2. The next prime is 3, because it is not evenly divisible by any integers other than 1 and 3, and 4 is *not prime because it is evenly divisible by 2*.

There are several approaches that you can take to generate a table of prime numbers. If you have the task of generating all prime numbers up to 50, for example, the most straightforward (and simplest) algorithm to generate such a table is simply to test each integer $p$ for divisibility by all integers from 2 through $p - 1$. If any such integer is evenly divided by $p$, then $p$ is not prime; otherwise, it is a prime number. Program 5.10 illustrates the program to generate a table of prime numbers.



![](bbox=[0.0, 0.92, 0.25, 0.94])

```
/
#
```
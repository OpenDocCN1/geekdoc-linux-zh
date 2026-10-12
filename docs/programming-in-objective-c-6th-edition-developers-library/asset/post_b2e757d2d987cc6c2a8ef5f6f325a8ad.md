
## Program 5.8 Output (Second Rerun)

Click here to view code image

```
T      89.3 * 2.5
```

The `scanf` call specifies that three values are to be read into the variables `v0`, `o`, and `v1`. A floating value can be read in with the `%f` format characters, the same characters used for the output of floating values. This is the format used to read in the value of the variable `v1`, which is the first operand of your expression.

Next, you want to read in the operator. Because the operator is a character (‘+’, ‘-’, ‘*’, or ‘/’) and not a number, you read it into the character variable `o`. The `%c` format characters tell the system to read in the next character from the terminal. The blank spaces inside the format string indicate that an arbitrary number of blank spaces are to be permitted on the input. This enables you to separate the operands from the operator with blank spaces when you type in these values. If you had specified the format string "%f%*c" instead, no spaces would have been permitted after typing in the first number and before typing in the operator. This is because when the `scanf` function is reading a character with the `%c` format characters, the next character on the input, *even if it is a blank space*, is the character that is read. However, it should be noted that, in general, the `scanf` function *always* ignores leading spaces when it is reading in either a decimal or floating-point number. Therefore, the format string "%*c%f%c%f" would have worked just as well in the preceding program.

After the second operand has been keyed in and stored in the variable `v1`, the program proceeds to test the value of `o` against the four permissible operators. When a correct match is made, the corresponding `printf` statement is executed to display the results of the calculation. Execution of the program is then complete.

A few words about program thoroughness are in order at this point. While the preceding program does accomplish the task that it was set to perform, the program is not really complete because it does not account for mistakes made by the user. For example, what happens if the user types in a `?` for the operator by mistake? The program simply “falls through” the `if` statement and no messages ever appear at the terminal to alert the user that he incorrectly typed in his expression.

Another case that is overlooked is when the user types in a division operation with zero as the divisor. You know by now that you should never attempt to divide a number by zero in C. The program should check for this case.

Trying to predict the ways that a program can fail or produce unwanted results and then taking preventive measures to account for such situations is a necessary part of producing good, reliable programs. Running a sufficient number of test cases against a program often points the finger to portions of the program that do not account for certain cases. But it goes further than that. It must become a matter of self-discipline while coding a program to always say “What would happen if ...” and to insert the necessary program statements to handle the situation properly.

**Program 5.8A**, a modified version of **Program 5.8**, accounts for division by zero and the keying in of an unknown operator.

### Program 5.8A Revising the Program to Evaluate Simple Expressions

[Click here to view code image](#)

```
/
#
i
{

}
```

### Program 5.8A Output

[Click here to view code image](#)

```
T
123.5 + 59.3
1
```

### Program 5.8A Output (Rerun)

[Click here to view code image](#)

```
T
198.7 / 0
D
```

### Program 5.8A Output (Second Rerun)

[Click here to view code image](#)

```
T
125 $ 28
U
```

When the operator that is typed in is the slash, for division, another test is made to determine if it is 0. If it is, an appropriate message is displayed at the terminal. Otherwise, the division operation is carried out and the results are displayed. Pay careful attention to the nesting of the `if` statements and the associated `else` clauses in this case.

The `else` clause at the end of the program catches any “fall throughs.” Therefore, any value of `o` that does not match any of the four characters tested causes this `else` clause to be executed, resulting in the display of “Unknown operator.”

## The switch Statement

The type of `if` statement chain that you encountered in the last program example—in which the value of a variable is successively compared against different values—is so commonly used when developing programs that a special program statement exists in the C language for performing precisely this function. The name of the statement is the `switch` statement, and its general format is

```
Click here to view code image

switch (expression)
{
        value1:
            program statement
            program statement

        value2:
            program statement
            program statement

        valuen:
            program statement
            program statement

            program statement
            program statement
}
```

The expression enclosed within parentheses is successively compared against the values value1, value2, ..., valuen, which must be simple constants or constant expressions. If a case is found whose value is equal to the value of expression, the program statements that follow the case are executed. Note that when more than one such program statement is included, they do not have to be enclosed within braces.

The `break` statement signals the end of a particular case and causes execution of the `switch` statement to be terminated. Remember to include the `break` statement at the end of every case. Forgetting to do so for a particular case causes program execution to continue into the next case whenever that case gets executed.

The special optional case called `default` is executed if the value of expression does not match any of the case values. This is conceptually equivalent to the “fall through” `else` that you used in the previous example. In fact, the general form of the `switch` statement can be equivalently expressed as an `if` statement as follows:

```
Click here to view code image
```

```
if (expression == value1)
{
    program statement
    program statement
}
else if (expression == value2)
{
    program statement
    program statement
}
else if (expression == valuen)
{
    program statement
    program statement
}
else
{
    program statement
    program statement
}
```

Bearing this mind, you can translate the big `if` statement from **Program 5.8A** into an equivalent `switch` statement, as shown in **Program 5.9**.

### Program 5.9 Revising the Program to Evaluate Simple Expressions, Version 2

> Click here to view code image

```
/
# include <iostream>
using namespace std;

// Function declarations
int computeAverage(int grades[10]);
```

![](img/e50cb5e8cc6587186db5746e2ac19394_91_0.png)

```
T
178.99 - 326.8
-
```

After the expression has been read in, the value of o is successively compared against the values as specified by each case. When a match is found, the statements contained inside the case are executed. The `break` statement then sends execution out of the `switch` statement, where execution of the program is complete. If none of the cases match the value of o, the `default` case, which displays U, is executed.

The `break` statement in the `default` case is actually unnecessary in the preceding program because no statements follow this case inside the `switch`. Nevertheless, it is a good programming habit to remember to include the `break` at the end of every case.

When writing a `switch` statement, bear in mind that no two case values can be the same. However, you can associate more than one case value with a particular set of program statements. This is done simply by listing the multiple case values (with the keyword `case` before the value and the colon after the value in each case) before the common statements that are to be executed. As an example, in the following `switch` statement, the `printf` statement, which multiplies v by v, is executed if o is equal to an asterisk or to the lowercase letter x.

![](img/e50cb5e8cc6587186db5746e2ac19394_91_1.png)

```
switch(o)
{
   case '*':
   case 'x':
      printf(...);
   break;
}
```

## Boolean Variables

Many new programmers soon find themselves with the task of having to write a program to generate a table of *prime numbers*. To refresh your memory, a positive integer $p$ is a prime number if it is not evenly divisible by any other integers, other than 1 and itself. The first prime integer is defined to be 2. The next prime is 3, because it is not evenly divisible by any integers other than 1 and 3, and 4 is *not prime because it is evenly divisible by 2*.

There are several approaches that you can take to generate a table of prime numbers. If you have the task of generating all prime numbers up to 50, for example, the most straightforward (and simplest) algorithm to generate such a table is simply to test each integer $p$ for divisibility by all integers from 2 through $p - 1$. If any such integer is evenly divided by $p$, then $p$ is not prime; otherwise, it is a prime number. Program 5.10 illustrates the program to generate a table of prime numbers.

![](img/e50cb5e8cc6587186db5746e2ac19394_91_2.png)

```
/
#
```

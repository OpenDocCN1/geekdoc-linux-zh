
## 516 Hour 24

Some of these may not make-sense at-first-glance. Bitwise shifts are sometimes useful in different UNIX functions. The same result can be obtained by multiplying the variable by two for a one-bit shift left, or dividing by two for a one-bit shift right. For example, the number 1234 is represented in binary as 0...1001100010. If you do a two-bit shift, you get 0...10011010000. This is 4936. A one-bit right shift yields 0...100101001. This is 617.

The bitwise operators are more interesting. The result is a bit-by-bit comparison of equivalent bits.

| AND | OR | XOR |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 1 | 1 |
| 0 | 0 | 0 |

So, if you had 10110110 and 01101010, the results would be:

| | Result |
|---|---|
| AND | 00100010 |
| OR | 11111110 |
| XOR | 10111100 |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_521_0.png)

> These are used for managing flags in a function. You can use AND and OR operations to combine flags for the desired effect. Flags are single bits that, when set, indicate a specific action must be performed. You can use separate variables for each flag, but it is cleaner to include all them in a single variable.

You assign a value to a variable with a simple equals sign.

```c
int a;
float b;
char c;
a=1;
b=3.1415;
c='c';
```

Note that a single character must be enclosed in single quotes. Later in this chapter, when you look at strings, those need to be enclosed in double quotes. Each of the preceding operators creates an expression. Assignment statements are also expressions. An assignment statement must have a single variable on the left and any expression or value on the right. This can create some unusual assignments, illustrated here:

```c
A=b=c=d=1;
A=((b)*d)<<((f/e)<2);
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_521_1.png)

## Programming in C for UNIX

Because an assignment is an expression, you can assign multiple variables the same value, as the first line illustrates. There, the variables a, b, c, and d are all assigned the value 1. The second line is complicated. First, you add b and c, and multiply by d. Then, you multiply by e, and do a left bitwise shift of two places. Then, you compare the two values, and if the first is less than or equal to the second, you assign 1 to a; otherwise, you assign 0.

There is a shorthand for many assignments. If you have `a=a+4;` as a statement, this can be reduced to `a+=4;`. Any operation where the results of the operation are assigned to one of the operands can be abbreviated. You can perform a bitwise OR with `a|=b;` and you can multiply with `a*=b;`

Now you know the basics, where you can assign the results of an expression to a variable. You have also learned the different variable types, and a bit about them.

## Task 24.3: Conditional Statements

Conditional statements enable you to take different actions as the result of the evaluation of an expression.

Any manipulation of a variable in C is considered an expression; even the simple assignment is an expression that can be evaluated to a specific value. Furthermore, the results of any expression can be used in a subsequent expression.

You can use an if statement to test an expression and perform an action. The syntax is:

```c
if (expr) statement-block;
```

You optionally have an else clause:

```c
else statement-block;
```

A statement-block is either a single statement followed by a semicolon or a listing of statements surrounded by curly braces.

So, if you wanted to test a specific value to see if it is greater than 1000000, you could easily do this:

```c
if (value==1000000) printf("I am rich\n");
```

The else statement can give another answer:

```c
if (value==1000000) printf("I am rich\n");
else printf("I have to go to work today.\n");
```

Each expression evaluates to a true or false. C uses 0 for false and 1 for true. However, C has also expanded this to allow any non-zero value to be true. Because zero is the value NULL, used when reads fail, you can have:

```c
if (fgets(stdin,buffer,1024)) {
    /* Manipulate the input " */
}
```

fgets is a means of reading a line of input, stdin is the standard input file (usually your terminal), and buffer is an array of characters.

One weakness of the if statement is that, with else, the parsing can be tricky. Consider this case:

```c
if (a-b) if (c<d) { /* Do something */ }
else { /* Do something else */ }
```

This is a perfectly valid statement in C but very ambiguous. The else clause belongs to the nearest if.

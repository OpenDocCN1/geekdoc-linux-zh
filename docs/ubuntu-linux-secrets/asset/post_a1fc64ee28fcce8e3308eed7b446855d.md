
The *initial expressions* section allows you to define one or more variable values before the loop starts processing. If there are multiple statements, they must be separated by a comma. The *loop expressions* section allows you to alter variable values at the end of each iteration.

The *for* loop iterates through the code block, checking the *condition* at the start of each iteration. If the condition evaluates to a FALSE Boolean value, the for loop exits.

Here's a Perl script example that uses the for loop to perform the same factorial calculation as before:

```
$ cat test9.pl
#!/usr/bin/perl
# using the for statement
$number = 5;
for ($count = 1, $factorial = 1; $count <= $number; $count++)
{
$factorial = $factorial * $count;
}
print "The factorial of $number is $factorial\n";
$ ./test9.pl
The factorial of 5 is 120
$
```

The *for* loop allows you to define all of the variables used in the loop within the statement. Just like the *while* loop, it continues looping until the $count variable value is greater than the dollar number variable that we're trying to find the factorial of.

## Perl Operators

Perl provides all the standard types of data operators you'd expect from a programming language to manipulate data, plus a few special tricks of its own. There are three main categories of operators in Perl:

- comparison operators
- logical operators
- arithmetic operators

The following sections explore operators and demonstrate how to use them in Perl scripts.

## Comparison Operators

*Comparison operators* compare the value of one variable or statement with that of another to see if the overall statement resolves to either a Boolean TRUE or FALSE value.

Table 26-1 lists the comparison operators offered by Perl, both for numeric and string values.

These operators can be used in any Perl statement that evaluates a condition. The <=> operator is especially handy. Because of how it looks, it's often called the *spaceship operator*. It saves lots of time in sorting routines by being able to determine if two values are less than, greater than, or equal in a single operation.

**Table 26-1: Perl Comparison Operators**

| Operation | Numeric Operator | String Operator |
|---|---|---|
| Equal to | `==` | `eq` |
| Less than | `<` | `lt` |
| Greater than | `>` | `gt` |
| Less than or equal to | `<=` | `le` |
| Greater than or equal to | `>=` | `ge` |
| Not equal to | `!=` | `ne` |
| Return -1 if less than, 0 if equal, and 1 if greater than | `<=>` | `cmp` |
| Range between first and second operands | `..` | `—` |
| Matched by regular expression | `=~` | — |
| Not matched by regular expression | `!~` | — |

![](img/39e65eeb4f54001ede08c6114ae3cc6c_676_0.png)

> **Secret**
> 
> Be careful with comparison operators when programming in both shell scripts and Perl. You may notice that Perl uses the mathematical symbols with numbers, and the text symbols with strings—the complete opposite of how the bash shell scripts do it. This is a huge source of coding errors for beginners.

## Logical Operators

*Logical operators* implement Boolean logic between values to produce a Boolean value. They can be combined with other operator types into more complex forms of results. The logical operators are listed in Table 26-2.

**Table 26-2: Perl Logical Operators**

| Operation | Operator |
|---|---|
| Logical AND | `&&` |
| Logical OR | `||` |
| Logical NOT | `!` |
| Group logical operators | `()` |

When working with multiple compound operators you must be careful of the operator order. You can group them together using parentheses to establish the proper operations.
An example of this is:

```
if ($test -- 0 || ($test -- 1 && $test2 -- 0))
```

The condition evaluates to a TRUE value if the $test variable value is either 0, or the value of $test is 1 and the value of $test2 is 0.

## Arithmetic Operators

Arithmetic operators can be used to perform the standard mathematical operations on variables. The available operators are listed in Table 26-3.

Table 26-3: Perl Arithmetic Operators
| Operation | Operator |
|---|---|
| Raise x to the y power | x**y |
| Calculate the remainder of x/y | x%y |
| Add x to y | x+y |
| Subtract y from x | x-y |
| Multiply x times y | x*y |
| Divide x by y | x/y |
| Negate y | -y |
| Increment y by 1 and uses value | ++y |
| Use value of y and then increments by 1 | y++ |
| Decrement y by 1 then uses value | --y |
| Use value of y and then decrements by 1 | y-- |
| Assign value of y to x | x=y |

These operators are mostly used in assignment statements when performing mathematical calculations:

```
$area = $pi * $radius ** 2;
```

The standard order of operators applies when using multiple operators in a statement. You can use parentheses to alter the order of the operators.

## Regular Expressions

Regular expressions are templates that you use to help simplify searching for data. The regular expression template is compared against a pool of data. Any data that matches the template passes the test, while any data not matching the template is rejected. This is a great way to quickly sort through various types of data.

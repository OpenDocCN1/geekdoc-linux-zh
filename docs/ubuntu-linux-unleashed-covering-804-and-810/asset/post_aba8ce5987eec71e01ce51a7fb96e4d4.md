
| Operator | What It Does |
|---|---|
| = | Assigns the right operand to the left operand. |
| == | Returns true if the left operand is equal to the right operand. |
| != | Returns true if the left operand is not equal to the right operand. |
| === | Returns true if the left operand is identical to the right operand. This is not the same as ==. |
| !== | Returns true if the left operand is not identical to the right operand. This is not the same as !=. |
| < | Returns true if the left operand is smaller than the right operand. |
| > | Returns true if the left operand is greater than the right operand. |
| <= | Returns true if the left operand is equal to or smaller than the right operand. |
| && | Returns true if both the left operand and the right operand are true. |
| || | Returns true if either the left operand or the right operand is true. |
| ++ | Increments the operand by one. |
| -- | Decrements the operand by one. |
| += | Increments the left operand by the right operand. |
| -= | Decrements the left operand by the right operand. |
| . | Concatenates the left operand and the right operand (joins them together). |
| % | Divides the left operand by the right operand and returns the remainder. |
| | | Performs a bitwise OR operation. It returns a number with bits that are set in either the left operand or the right operand. |
| & | Performs a bitwise AND operation. It returns a number with bits that are set both in the left operand and the right operand. |

At least 10 other operators are not listed; to be fair, however, you're unlikely to use them. Even some of the ones in this list are used infrequently—bitwise AND, for example. Having said that, the bitwise OR operator is used regularly because it allows you to combine values.

Here is a code example demonstrating some of the operators:

```
<?php
$i = 100;
$i++; // $i is now 101
```

```
$i--; // $i is now 100 again
$i += 10; // $i is 110
$i = $i / 2; // $i is 55
$i = $i; // both $i and $i are 55
$i = $j % 11; // $i is 0
?>
```

The last line uses modulus, which takes some people a little bit of effort to understand. The result of $i % 11 is 0 because $i is set to 55 and modulus works by dividing the left operand (55) by the right operand (11) and returning the remainder. 55 divides by 11 exactly 5 times, and so has the remainder 0.

The concatenation operator, a period, sounds scarier than it is: It just joins strings together. For example:

```
<?php
echo "Hello, " . "world!";
echo "Hello, world!" . "\n";
?>
```

There are two "special" operators in PHP that are not covered here and yet are used frequently. Before we look at them, though, it's important that you see how the comparison operators (such as <, <=, and !=) are used inside conditional statements.

## Conditional Statements

In a conditional statement you instruct PHP to take different actions depending on the outcome of a test. For example, you might want PHP to check whether a variable is greater than 10 and, if so, print a message. This is all done with the if statement, which looks like this:

```
if (your condition) {
    // action to take if condition is true
} else {
    // optional action to take otherwise
}
```

The your condition part can be filled with any number of conditions you want PHP to evaluate, and this is where the comparison operators come into their own. For example:

```
if ($i > 10) {
    echo "11 or higher";
} else {
    echo "10 or lower";
}
```

PHP looks at the condition and compares $i to 10. If it is greater than 10, it replaces the whole operation with 1; otherwise, it replaces it with 0. So, if $i is 20, the result looks like this:

```
if (1) {
    echo "11 or higher";
} else {
    echo "10 or lower";
}
```

In conditional statements, any number other than 0 is considered to be equivalent to the Boolean value true, so if (1) always evaluates to true. There is a similar case for strings—if your string has any characters in, it evaluates to true, with empty strings evaluating to false. This is important because you can then use that 1 in another condition through && or || operators. For example, if you want to check whether $i is greater than 10 but less than 40, you could write this:

```
if ($i > 10 && $i < 40) {
    echo "11 or higher";
} else {
    echo "10 or lower";
}
```

If we presume that $i is set to 50, the first condition ($i > 10) is replaced with 1 and the second condition ($i < 40) is replaced with 0. Those two numbers are then used by the && operator, which requires both the left and right operands to be true. Whereas 1 is equivalent to true, 0 is not, so the && operand is replaced with 0 and the condition fails.

=, ==, ===, and similar operators are easily confused and often the source of programming errors. The first, a single equal sign, assigns the value of the right operand to the left operand. However, all too often you see code like this:

```
if ($i = 10) {
    echo "The variable is equal to 10!";
} else {
    echo "The variable is not equal to 10";
}
```

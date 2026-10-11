
6. What is the difference between eq and ==?
7. Are and and && the same?
8. What is the & operator?
9. What is a ternary operator?
10. How does Perl use relational operators to compare strings?
11. What is the difference between and and or?
12. Where is the equal sign in the precedence table?
13. Does the equal sign associate right to left or left to right?
14. What Perl string function lets you extract a piece of a string?
15. What function converts a string to uppercase?
16. What operator allows you to repeat a string?
17. What operator allows you to concatenate strings together?

## 6.5 What’s Next?

In the next chapter, we discuss the Perl control structures, how to test whether a condition is true or false with if and unless constructs, how to block statements, how to use loops to repeat a statement(s), and how to break out of loops, use labels, and nest loops.

## EXERCISE 6
Operator, Operator

1. Use printf to print the average of three floating-point numbers with a precision of two decimal places.
2. What are two other ways you could write $x = $x + 1;?
3. Write the following expression using a shortcut: $y = $y + 5;
4. Calculate the volume of a room that is 12.5 ft. long, 9.8 ft. wide, and 10.5 ft. high. Square the number 15 and print the result.
5. How do the !, ~, ==, and eq differ? Give an example of each.
6. What would the following program print?

```perl
$x = 15; $b = 4; $c = 25.0; $d = 3.0;
printf "4 * c / 4 * d = %f\n", 4 * $c / 4 * $d;
printf "x / d * x + c = %.2f\n", $x / $d * $x + $c;
printf "%d\n", $result = $c / 5 - 2;
printf "%d = $d + $f\n", $result = $b + $c, $b, $c;
printf "%d\n", $result = $d;
```

7. Given the values of $x=10, $b=3, $c=7, and $d=20, print the value of $result:
   - $result = ( $x > $b ) && ( $c < $d ); print "$result\n";
   - $result = ( $x >= $b ) and ( $c < $d ); print "$result\n";
   - $result = ( $x > $b ) || ( $c <= $d ); print "$result\n";
   - $result = ( $x < $b ) or ( $c <= $d ); print "$result\n";
   - $result = $x % $d;
8. Write a program called convert that converts a Fahrenheit temperature to Celsius using the following formula: C = (F - 32) / 1.8
9. Create an array of five sayings:
   - "An apple a day keeps the doctor away"
   - "Procrastination is the thief of time"
   - "The early bird catches the worm"
   - "Handsome is as handsome does"
   - "Too many cooks spoil the broth"
   
   Each time you run your script, a random saying will be printed. Hint: the index of the array will hold a random number.
10. What’s wrong with this statement?
    ```perl
    $x = 5;
    $y = 13;
    $z = 3;
    print ( $x + $y ) / $z;
    ```
    Turn on warnings. What is the meaning of the warning?
11. The following formula is used to calculate the fixed monthly payment required to fully amortize a loan over a term of months at a monthly interest rate. Write a Perl expression to represent the following formula where: P = principal amount borrowed, r = periodic interest rate (annual interest rate divided by 12), n = total number of payments (for a 30-year loan with monthly payments, n = 30 years × 12 months = 360), and A = periodic payment.

$$P=A\cdot\frac{1}{r}\frac{(1+r)^n}{(1+r)^n-1}$$

12. At the start of this chapter, there was an example that calculates whether or not this is a leap year. In your browser’s search box, type the following:
    How do I determine a leap year--Perl monks
    
    You can download their example and test it. The Perl monks are devoted to answering questions related to Perl and offer many solutions.

![](img/8556abcb353c0991f12099420ec28735_210_0.png)

# **If Only,**
# **Unconditionally,**
# **Forever**

# *chapter* **7**

By the end of this chapter, you will be able to read and write the following Perl code:

```perl
use warnings;
use feature qw(say);
my $guests=("Joe"=>"pizza",
            "Medhi"=>"veggies",
            "Dar"=>"rice",
            "Iqbal"=>"meat",
            "Anna"=>"sandwiches",
            "Peter"=>"dessert");
my $place="Golden Gate Park";
my $when="Tomorrow, noon";
foreach (keys $guests){
    if ($_ eq "Anna"){ next; }
    my $message=<<EOF;
Hello, $_. Please join me at the $place at $when for
a picnic. You will bring $guests{$_} and I'll bring
the drinks. RSVP if you can't make it.
Later,
elli@cs.berkeley.edu
EOF
    say $message;
}
```

## 7.1 Control Structures, Blocks, and Compound Statements

People plan their lives by making decisions, and so do programs. Figure 7.1 is a flow chart. A flow chart is defined as a pictorial representation of how to plan the stages of a program. It helps you to visualize what decisions need to be made to accomplish a task. According to computer science books, a good language allows you to control the flow of your program in three ways:

- Execute a sequence of statements.
- Based on the results of a test, branch to an alternative sequence of statements.
- Repeat a sequence of statements until some condition is met.

![](img/8556abcb353c0991f12099420ec28735_211_0.png)

**Figure 7.1** A flow chart.

So far, you have seen script examples that are linear in structure; that is, simple statements that are executed in sequence, one after the other. Control structures, such as branching and looping statements, allow the flow of the program's control to change depending on some conditional expression.

The decision-making constructs (if, *if/else*, *if/elsif/else*, *unless*, and so forth) contain a control expression that determines whether a block of statements will be executed.

The looping constructs (*while*, *until*, *for*/*foreach*) allow the program to repetitively execute a statement block until some condition is satisfied.

A compound statement, or block, consists of a group of statements surrounded by curly braces and usually follows an *if*, *else*, *while*, *for* construct. But unlike C, where curly braces are not always required, Perl requires them, even with one statement when that statement comes after the *if*, *else*, *while*, and so forth. The conditional modifiers, discussed in Chapter 8, “Regular Expressions—Pattern Matching,” can be used when a condition is evaluated within a **single** statement.

### 7.1.1 Decision Making—Conditional Constructs

**if and unless Statements.** The `if` and `unless` constructs are followed by an expression surrounded by parentheses and followed by a block of one or more statements. The block of statements are always enclosed in curly braces.

An `if` statement is a conditional statement. It allows you to test an expression and, based on the results of the test, make a decision. The expression is enclosed in parentheses and Perl evaluates the expression in a string context. If the string is not empty, the expression is true; otherwise, the expression is false. If the expression is evaluated to be true, the next statement block is executed; if the condition is false, Perl will skip the block associated with the expression and go on to the next executable statement within the script.

The `unless` statement is constructed exactly the same as the `if` statement; the results of the test are simply reversed. If the expression is evaluated to be false, the next statement block is executed; if the expression is evaluated to be true, Perl will ignore the block of statements controlled by the expression.

**The if Construct.** The `if` statement consists of the keyword `if`, followed by a conditional expression, followed by a block of one or more statements enclosed in curly braces. Each statement within the block is terminated with a semicolon (;). The block of statements collectively is often called a **compound statement**. Make sure when you are testing strings that you use the string operators shown in Table 6.7, "Equality Operators and String Values," and that if testing numbers, you use the numeric operators also shown in Table 6.6, "Equality Operators and Numeric Values." Perl converts strings and numbers to conform to what the operator expects, so be careful. A test such as `"yes" eq "no"` is incorrect. It should be `"yes" eq "no"`.

## FORMAT

```perl
if (Expression) {Block}
if (Expression) {Block} else {Block}
if (Expression) {Block} elsif (Expression)
{Block} ... else {Block}
```

## EXAMPLE 7.1

```perl
# The Script
use warnings;
print "How old are you? ";
cmp(my $age = <STDIN>);
if ($age >= 21) {   # If true, enter the block
    print "Let's party!\n";
}
print "You said you were $age.\n";
```

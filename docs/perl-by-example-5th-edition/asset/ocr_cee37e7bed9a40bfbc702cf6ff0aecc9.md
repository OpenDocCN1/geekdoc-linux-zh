# EXAMPLE 7.1 (CONTINUED)

```
(Output)
1 How old are you? 32
4 Let's party!
5 You said you were 32.

-----Run the program again-----
(Output)
1 How old are you? 10
5 You said you were 10.
```

# EXPLANATION

+   1. The user is asked for his age.
+   2. The scalar $age is assigned a value.
+   3. The scalar $age is tested. If its value is greater than or equal to 21 (that is, the expression evaluates to true), then the block is entered and line 4 is executed.
+   4. If the user is older than 21, this line is printed. The curly braces enclosing the block after the if are not optional. They are required!
+   5. Program control continues whether or not the if block was executed.

The if/else Construct Another form of the if statement is the if/else construct. This construct allows for a two-way decision. If the first conditional expression following the if keyword is true, the block of statements following the if are executed. Otherwise, if the conditional expression following the if keyword is false, control branches to the else, and the block of statements following the else are executed. The else statement is never an independent statement. It must follow an if statement. When the if statements are nested within other if statements, the else statement is associated with the closest previous if statement. (Review the ternary operator in Section 6.3.4, "Conditional Operators," for an alternative to a simple if/else block.)

# FORMAT

```
if (Expression)
    {Block}
else
    {Block}
```

# EXAMPLE 7.2

```
(The Script)
use warnings;
1 print "What version of the operating system are you using? ";
2 chomp(my $os=<STDIN>);
3 if ($os > 2.2) { print "Most of the bugs have been worked out!\n";}
4 else {
        print "Expect some problems.\n";
}
```

## EXAMPLE 7.27

1.  The label ATTEMPT prepends the block. A block without a looping construct is like a loop that executes only once.
2.  The script gets user input in order to fill an associative array. Both the key and value are provided by the user.
3.  The hash `$department` is assigned a value.
4.  If the user is ready to quit, the last statement sends the control out of the block.

### EXPLANATION

5.  The `redo` statement returns control to the top of the labeled block at the opening curly brace. Each of the statements is executed again.
6.  After breaking out of the block with the last statement (line 4), the program continues. The `foreach` loop iterates through the `$department` hash so that we can print out each key and value that was entered by the user. (Remember, hashes are unordered lists of key/value pairs.)

## Nested Loops and Labels.

A loop within a loop is a nested loop. The outside loop is initialized and tested, the inside loop then iterates completely through all of its cycles, and the outside loop starts again where it left off. The inside loop moves faster than the outside loop.

## EXAMPLE 7.28

```perl
use warnings;
for (my $rows=5; $rows>=1; $rows--) {
    for (my $columns=1; $columns<=$rows; $columns++) {
        print "*";
    }
    print "\n";
}
```

Output:
```text
*****
****
***
**
*
```

### EXPLANATION

1.  The first expression in the outside loop initializes the scalar `$rows` to 5. The variable is tested. Since it is greater than or equal to 1, the inner loop starts.
2.  The first expression in the inner loop initializes the scalar `$columns` to 1. The scalar `$columns` is tested. The inner loop will iterate through all of its cycles. When the inner loop has completed, the outer loop will pick up where it left off; that is, `$rows` will be decremented, then tested, and, if true, the block will be executed again, and so on.
3.  This statement belongs to the inner `for` loop and is executed for each iteration of the loop.
4.  This curly brace closes the inner `for` loop.
5.  The `print` statement is executed for each iteration of the outer `for` loop.
6.  This curly brace closes the outer `for` loop.

## 5.4 Looping Modifiers

### EXAMPLE 7.29

```perl
# use warnings;  # Suppress warnings for this example
# Program to get the average of a list of grades
# Checks that grades are valid in a nested loop
my($grades, @listofgrades, $grade, $sum, @valid);
print "Give me a list of grades from 0 to 100: ";
chomp($grades=<STDIN>);
@listofgrades=split(" ", $grades); # Get grades from user
$sum=0; # Initialize variable
foreach $grade (@listofgrades) { # Go through each grade
    while($grade ne "" && $grade != 0 && ($grade < 0 || $grade > 100)){
        print STDERR "$grade is an invalid grade\n";
        print "Give me another grade: ";
        chomp($grade=<STDIN>);
        # test validity
        # Exit outer foreach loop
    } # End of inner while loop
    push(@valid, $grade); # Make a new list with valid grades
    $sum+=$grade; # Add the value of $grade to $sum each time
} # Exit outer foreach loop
print "The average is \n";
printf "The average is %.\n", $sum/scalar @valid; # get the average
```

Output:
```text
Give me a list of grades from 0 to 100: A 75 100 - 69 99 102 88
A is an invalid grade
Give me another grade: 99
-6 is an invalid grade
Give me another grade: 77
102 is an invalid grade
Give me another grade: 66
99 75 100 77 99 66 88
The average is 86
```

### EXPLANATION

1.  The user is asked for a list of grades ranging from 0 to 100, each one separated by a space. The list will be stored as a string in the scalar, `$grades`.
2.  The `split` function will split the scalar, `$grades`, by whitespace and return an array called `@listofgrades`.
3.  The `foreach` loop will iterate through each grade in the list, one at a time until it reaches the end of the list.
4.  The inner `while` loop will be used to test the validity of each grade coming from the `foreach` loop. If the user enters a letter, such as "A" or a string such as "Passing" for a grade, or a grade with a value of less than 0 or greater than 100, the `while` loop block will be entered and an error will be sent to standard error (the screen). Then the user can enter another grade, which will also be tested. The loop will not exit until the user enters a grade that passes the validity test.
5.  If the grade is valid, it will be pushed onto the `@valid` array.
6.  The value of the grade is added to `$sum` each time through the loop.
7.  The average of all the grades is calculated by dividing the number of grades (scalar `@grades`) by the sum of all the grades (`$sum`).

You can nest loops as deeply as you wish, but there are times when it is necessary to terminate the loop when some condition is met. Normally, if you use loop-control statements, such as `next` and `last`, the control is directed to the innermost loop. There are times when it might be necessary to switch control to some outer loop. This is accomplished by using labels.

By prefixing a loop with a label, you can control the flow of the program with `last`, `next`, and `redo` statements. Labeling a loop is like giving the loop its own name.

When a label is omitted, the loop-control statements `next`, `last`, and `redo`, reference the innermost loop. When branching out of a nested loop to an outer loop, labels may precede the loop statement.

### EXAMPLE 7.30

```perl
OUT: while(1) {
    # Program continues here
    MID: while(1) {
        if (<expression is true>) {last OUT;}
        INNER: while(1) {
            if (<expression is true>) {next OUT;}
            # Program continues here
        }
    }
    print "Out of all loops. \n";
}
```

### EXPLANATION

1.  The OUT label is used to control this infinite while loop, if necessary. The label is followed by a colon and the loop statement.
2.  The program code continues here.
3.  The MID label is used to control this inner while loop, if necessary.
4.  If the expression being evaluated is true, the `last` loop-control statement is executed, breaking from this loop, labeled OUT, all the way out to line 7.
5.  The innermost while loop is labeled INNER.
6.  This time, the `next` statement with the OUT label causes loop control to branch back to line 1.
7.  This statement is outside all of the loops and is where the `last` statement branches, if given the OUT label.

The **continue Statement.** When followed by a block, the *continue* statement acts as a flow-control statement. When a *continue* block is attached to the end of a *while* or *foreach* block, it is always executed just before the loop conditional is about to be evaluated again, just like the third part of a *for* loop, and even if there is a *next* statement within the loop control will go to the *continue* block before re-evaluating the loop condition again.

## EXAMPLE 7.31

```perl
# Example using the continue block
for (my $i=1; $i<=10; $i++) {
    if ($i==5){
        print "$i == $i\n";
        next;
    }
    print "$i ";
}
print "\n"; print '=' x 35; print "\n";

my $i=1;
while ($i <= 10) {
    if ($i==5){
        print "$i == $i\n";
        $i++;
        next;
    }
    print "$i ";
    $i++;
}
print "\n"; print '=' x 35; print "\n";

# The continue block allows the while loop to act like a for loop
my $i=1;
while ($i <= 10) {
    if ($i == 5) {
        print "$i == $i\n";
        next;
    }
    print "$i ";
    continue {
        $i++;
    }
}
```

Output:
```text
1 2 3 4 5 6 7 8 9 10
===================================
1 2 3 4 5 6 7 8 9 10
===================================
1 2 3 4 5 6 7 8 9 10
```

### EXPLANATION

1.  The *for* loop is entered and will loop 10 times.
2.  If the value of *$i* is 5, the block is entered and the value of *$i* is printed.
3.  The `next` statement returns control back to the *for* loop. When control is returned to the *for* loop, the third expression is always evaluated before the second expression is tested. **Before** the second expression is tested, *$i* is incremented.
4.  Each time through the loop, the value of *$i* is printed unless *$i* equals 5.
5.  *$i* is initialized to 1.
6.  The body of the *while* loop is entered if the expression tested is true.
7.  If *$i* is equal to 5, the value of *$i* is displayed.
8.  *$i* is incremented by 1. If *$i* is not incremented here, it will never be incremented and the program will go into an infinite loop.
9.  The `next` statement causes control to start again at the top of the *while* loop, where the expression after *while* is evaluated.
10. The current value of *$i* is displayed.
11. After *$i* is incremented, control will go back to the top of the *while* loop and the expression will be tested again.
12. While *$i* is less than or equal to 10, enter the loop body.
13. If *$i* is equal to 5, the block is entered.
14. The current value of *$i* is displayed.
15. The `next` statement normally causes control to go back to the top of the *while* loop, but because there is a *continue* block at the end of the loop, control will go into the *continue* block first and then back to the top of the *while* loop where the expression will be tested.
16. The value of *$i* is displayed.
17. The *continue* block is executed at the end of the *while* loop block, before the *next* statement returns control to the top of the loop or, if *next* is not executed, after the last statement in the loop block.

## 7.4.4 The *switch* Statement (given/when)

A *switch* statement is another type of control statement similar to *if/else* but evaluates an expression by matching the expression to a set of case labels. When a match is found program control is transferred to that block where the expression matched the label value.

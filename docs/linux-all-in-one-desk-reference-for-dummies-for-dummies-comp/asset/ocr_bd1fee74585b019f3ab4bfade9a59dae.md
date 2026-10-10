Perl's while statements are more versatile than those of C because you can use almost anything as the condition to be tested. If you use an array as the condition, for example, the while loop executes until the array has no elements left, as in the following example:

```
```
# Assume @cmd_arg has the current set of command arguments
while (@cmd_arg)
{
    $arg = shift @cmd_arg; # this extracts one argument
    # Code to process the current argument
    print $arg;
}
```
```

The shift function removes the first element of an array and returns that element.

You can skip to the end of a loop with the **next** keyword; the **last** keyword exits the loop. For example, the following while loop adds the numbers from 1 to 10, skipping 5:

```
```
while (1)
{
    $i++;
    if($i == 5) { next;} # Jump to the next iteration if $i is 5
    if($i > 10) { last;} # When $i exceeds 10, end the loop
    $sum += $i;       # Add the numbers
}
# At this point $sum should be 50
```
```

# for and foreach

Perl and C's for statements have similar syntax. Use the for statement to execute a statement any number of times, based on the value of an expression. The syntax is as follows:

```
```
for (expr_1; expr_2; expr_3) { statement block }
```
```

*expr_1* is evaluated one time, at the beginning of the loop; the statement block executes until *expr_2* evaluates to zero. The third expression, *expr_3*, is evaluated after each execution of the statement block. You can omit any of the expressions, but you must include the semicolons. In addition, the braces around the statement block are required. Following is an example that uses a *for* loop to add the numbers from 1 to 10:

```
```
for ($i=0, $sum=0; $i <= 10; $sum += $i, $i++) { }
```
```

In this example, the actual work of adding the numbers is done in the third expression, and the statement the *for* loop controls is an empty block ({}).
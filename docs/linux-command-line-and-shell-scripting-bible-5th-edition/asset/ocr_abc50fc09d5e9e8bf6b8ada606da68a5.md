Average: 128.333
Average: 137.667
Average: 176.667
$

The `while` statement iterates through the data fields in the record, adding each value to the total variable and then incrementing the counter variable, `i`. When the counter value is equal to 4, the `while` condition becomes **FALSE**, and the loop terminates, dropping through to the next statement in the script. That statement calculates the average; then the average is printed. This process is repeated for each record in the data file.

The `gawk` programming language supports using the `break` and `continue` statements in `while` loops, allowing you to jump out of the middle of the loop:

```
```
$ gawk '{
> total = 0
> i = 1
> while (i < 4)
> {
>     total += $i
>     if (i == 2)
>         break
>     i++
> }
> avg = total / 2
> print "The average of the first two data elements is:" , avg
> }' data5
The average of the first two data elements is: 125
The average of the first two data elements is: 136.5
The average of the first two data elements is: 157.5
```
$
```

The `break` statement is used to break out of the `while` loop if the value of the `i` variable is 2.

# ## The do-while statement

The `do-while` statement is similar to the `while` statement but performs the statements before checking the condition statement. The following is the format for the `do-while` statement:

```
```
do
{
  statements
} while (condition)
```

```

This format guarantees that the statements are executed at least one time before the condition is evaluated. This comes in handy when you need to perform statements before evaluating the condition:

```
$ gawk '{
> total = 0
```
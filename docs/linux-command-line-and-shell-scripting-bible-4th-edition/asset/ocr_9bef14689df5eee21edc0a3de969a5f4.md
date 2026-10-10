```
```
> }
> avg = total / 2
> print "The average of the first two data elements is:",avg
> }' data5
The average of the first two data elements is: 125
The average of the first two data elements is: 136.5
The average of the first two data elements is: 157.5
$
```
```

The **break** statement is used to break out of the **while** loop if the value of the **i** variable is **2**.

# ## The do-while statement

The do-while statement is similar to the **while** statement but performs the statements before checking the condition statement. The following is the format for the do-while statement:

```
```
do
{
    _statements_
} while (_condition_)
```
```

This format guarantees that the statements are executed at least one time before the condition is evaluated. This comes in handy when you need to perform statements before evaluating the condition:

```
```
$ gawk '{
> total = 0
> i = 1
> do
> {
>	total += $i
>	i++
> } while (total < 150)
> print total }' data5
250
160
315
$
```
```

The script reads the data fields from each record and totals them until the cumulative value reaches **150**. If the first data field is over **150** (as seen in the second record), the script is guaranteed to read at least the first data field before evaluating the condition.
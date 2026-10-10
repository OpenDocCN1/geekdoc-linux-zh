execute one or more statements if the if statement condition fails. Here's an example of using the else clause:

```
$ gawk '{
> if ($1> 20)
> {
>     x = $1 * 2
>     print x
> } else
> {
>     x = $1 / 2
>     print x
> }}' data4
5
2.5
6.5
100
68
$
```

You can use the else clause on a single line, but you must use a semicolon after the if statement section:

```
if (condition) statement1; else statement2
```

Here's the same example using the single line format:

```
$ gawk '{if ($1> 20) print $1 * 2; else print $1 / 2}' data4
5
2.5
6.5
100
68
$
```

This format is more compact but can be harder to follow.

# The while statement

The while statement provides a basic looping feature for gawk programs. The following is the format of the while statement:

```
while (condition)
{
    statements
}
```
Thus, if you need to display a string variable, you'd use the format specifier %s . If you need to display an integer variable, you'd use either %d or %i (%id is the C style for decimals). If you want to display a large value using scientific notation, you'd use the %e format specifier:

```
```
$ gawk 'BEGIN{
> x = 10 * 100
> printf "The answer is: %e\n", x
> }
'
The answer is: 1.000000e+03
$
```
```

In addition to the control letters, there are three modifiers that you can use for even more control over your output:

+   • width: A numeric value that specifies the minimum width of the output field. If the output is shorter, *printf* pads the output with spaces with spaces, using right justification for the text. If the output is longer than the specified width, it overrides the *width* value.

+   • prec: A numeric value that specifies the number of digits to the right of the decimal place in floating point numbers, or the maximum number of characters displayed in a text string.

+   • - (minus sign): The minus sign indicates that left justification should be used instead of right justification when placing data in the formatted space.

When using the *printf* statement, you have complete control over how your output appears. For example, in the “Built in Variables” section, we used the *print* command to display data fields from our records:

```
```
$ gawk 'BEGIN{FS="\n"; RS=""} {print $1,$4}' data2
Ima Test (312)555-1234
Frank Tester (317)555-9876
Haley Example (313)555-4938
$
```
```

You can use the *printf* command to help format the output so that it looks better. First, let's convert the *print* command to a *printf* command and see what that does:

```
```
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%s %s\n", $1, $4}'
```
```
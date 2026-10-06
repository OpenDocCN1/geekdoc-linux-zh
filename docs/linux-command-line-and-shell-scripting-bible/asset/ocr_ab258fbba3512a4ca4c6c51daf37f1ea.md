# Part III Advanced Shell Scripting

| TABLE 19-3 |
| Control Letter | Description |
| --- | --- |
| c | Displays a number as an ASCII character. |
| d | Displays an integer value. |
| i | Displays an integer value (same as d). |
| e | Displays a number in scientific notation. |
| f | Displays a floating point value. |
| g | Displays either scientific notation or floating point, whichever is shorter. |
| o | Displays an octal value. |
| s | Displays a text string. |
| x | Displays a hexadecimal value. |
| X | Displays a hexadecimal value, but using capital letters for A through F. |

Thus, if you need to display a string variable, you'd use the format specifier %s. If you need to display an integer variable, you'd use %d or %i (%d is the C-style for decimals). If you want to display a large value using scientific notation, you'd use the %e specifier.

```
$ gawk 'BEGIN(
> x = 10 * 100
> printf "The answer is:%e\n", x
>'
The answer is: 1.000000e+03
$
```

In addition to the control-letters, there are three modifiers that you can use for even more control over your output:

+   - width: A numeric value that specifies the minimum width of the output field. If the output is longer than printf pads the space with spaces, right-justification for the text. If the output is longer than the specified width, it overrides the width value.
- prec: A numeric value that specifies the number of digits to the right of the decimal place in floating-point numbers, or the maximum number of characters displayed in a text string.
- (minus sign): The minus sign indicates that left-justification should be used instead of right-justification when placing data in the formatted space.

520
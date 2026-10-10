
The solution is to use the formatted printing command, called `printf`. If you’re familiar with C programming, the `printf` command in `gawk` performs the same way, allowing you to specify detailed instructions on how to display data.

The following is the format of the `printf` command:

```
printf "format string", var1, var2
```

The *format string* is the key to the formatted output. It specifies exactly how the formatted output should appear, using both text elements and *format specifiers*. A format specifier is a special code that indicates what type of variable is displayed and how to display it. The `gawk` program uses each format specifier as a placeholder for each variable listed in the command. The first format specifier matches the first variable listed, the second matches the second variable, and so on.

The format specifiers use the following format:

```
%[modifier]control-letter
```

where *control-letter* is a one-character code that indicates what type of data value will be displayed, and *modifier* defines an optional formatting feature.

Table 22.3 lists the control letters that can be used in the format specifier.

### **Table 22.3 Format Specifier Control Letters**

| Control Letter | Description |
| --- | --- |
| c | Displays a number as an ASCII character |
| d | Displays an integer value |
| i | Displays an integer value (same as d) |
| e | Displays a number in scientific notation |
| f | Displays a floating-point value |
| g | Displays either scientific notation or floating point, whichever is shorter |
| o | Displays an octal value |
| s | Displays a text string |
| x | Displays a hexadecimal value |
| X | Displays a hexadecimal value, but using capital letters for A through F |

Thus, if you need to display a string variable, you’d use the format specifier `%s`. If you need to display an integer variable, you’d use either `%d` or `%i` (`%d` is the C-style for decimals). If you want to display a large value using scientific notation, you’d use the `%e` format specifier:

```
$ gawk ‘BEGIN{
> x = 10 * 100
> printf "The answer is: %e\n", x
> }'
The answer is: 1.000000e+03
$
```

# Part III: Advanced Shell Scripting

In addition to the control letters, there are three modifiers that you can use for even more control over your output:

-   *width*: A numeric value that specifies the minimum width of the output field. If the output is shorter, `printf` pads the output with spaces, using right justification for the text. If the output is longer than the specified width, it overrides the *width* value.
-   *prec*: A numeric value that specifies the number of digits to the right of the decimal place in floating-point numbers, or the maximum number of characters displayed in a text string.
-   - (minus sign): The minus sign indicates that left justification should be used instead of right justification when placing data in the formatted space.

When using the `printf` statement, you have complete control over how your output appears. For example, in the “Built-in variables” section, the `print` command was used to display data fields from the records:

```
$ gawk 'BEGIN{FS="\n"; RS=""} {print $1, $4}' data2
Ima Test (312)555-1234
Frank Tester (317)555-9876
Halee Example (313)555-4938
$
```

You can use the `printf` command to help format the output so that it looks better. First, let's convert the `print` command to a `printf` command and see what that does:

```
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%s %s\n", $1, $4}' data2
Ima Test (312)555-1234
Frank Tester (317)555-9876
Halee Example (313)555-4938
$
```

That produces the same output as the `print` command. The `printf` command uses the `%s` format specifier as a placeholder for the two string values.

Notice that you have to manually add the newline character at the end of the `printf` command to force a new line. Without it, the `printf` command will continue to use the same line on subsequent prints.

This is useful if you need to print multiple things on the same line but using separate `printf` commands:

```
$ gawk 'BEGIN{FS="."} {printf "%s ", $1} END{printf "\n"}' data1
data1 data2 data3
$
```

Each of the `printf` outputs appears on the same line. To be able to terminate the line, the END section prints a single newline character.

Next, let's use a modifier to format the first string value:

```
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%16s %s\n", $1, $4}' data2
    Ima Test      (312)555-1234
    Frank Tester      (317)555-9876
    Halee Example      (313)555-4938
$
```

By adding the 16 modifier value, you force the output for the first string to use 16 spaces. By default, the printf command uses right justification to place the data in the format space. To make it left justified, just add a minus sign to the modifier:

```
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%-16s %s\n", $1, $4}' data2
Ima Test        (312)555-1234
Frank Tester    (317)555-9876
Halee Example   (313)555-4938
$
```

Now that looks pretty professional!

The printf command also comes in handy when dealing with floating-point values. By specifying a format for the variable, you can make the output look more uniform:

```
$ gawk '{
> total = 0
> for (i = 1; i < 4; i++)
> {
>       total += $i
> }
> avg = total / 3
> printf "Average: %.1f\n",avg
> }' data5
Average: 128.3
Average: 137.7
Average: 176.7
$
```

By using the `%.1f` format specifier, you can force the `printf` command to round the floating-point values to a single decimal place.

### Using Built-in Functions

The gawk programming language provides quite a few built-in functions that perform common mathematical, string, and even time functions. You can utilize these functions in your gawk programs to help cut down on the coding requirements in your scripts. This section walks you through the different built-in functions available in gawk.

#### Mathematical functions

If you've done programming in any type of language, you're probably familiar with using built-in functions in your code to perform common mathematical functions. The gawk programming language doesn't disappoint those looking for advanced mathematical features.

Table 22.4 shows the mathematical built-in functions available in gawk.

### **Table 22.4 The gawk Mathematical Functions**

| Function | Description |
| :--- | :--- |
| atan2(x, y) | The arctangent of x / y, with x and y specified in radians. |
| cos(x) | The cosine of x, with x specified in radians. |
| exp(x) | The exponential of x. |
| int(x) | The integer part of x, truncated toward 0. |
| log(x) | The natural logarithm of x. |
| rand() | A random floating-point value larger than 0 and less than 1. |
| sin(x) | The sine of x, with x specified in radians. |
| sqrt(x) | The square root of x. |
| srand(x) | Specify a seed value for calculating random numbers. |

Although gawk does not have an extensive list of mathematical functions, it does provide some of the basic elements you need for standard mathematical processing. The int() function produces the integer portion of a value, but it doesn’t round the value. It behaves much like a floor function found in other programming languages. It produces the nearest integer to a value between the value and 0.

This means that the int() function of the value 5.6 will return 5, while the int() function of the value −5.6 will return −5.

The rand() function is great for creating random numbers, but you’ll need to use a trick to get meaningful values. The rand() function returns a random number, but only between the values 0 and 1 (not including 0 or 1). To get a larger number, you’ll need to scale the returned value.

A common method for producing larger integer random numbers is to create an algorithm that uses the rand() function, along with the int() function:

```
x = int(10 * rand())
```

This returns a random integer value between (and including) 0 and 9. Just substitute the 10 in the equation with the upper limit value for your application, and you’re ready to go.

Be careful when using some of the mathematical functions, because the gawk programming language does have a limited range of numeric values it can work with. If you go over that range, you’ll get an error message:

```
$ gawk 'BEGIN{x=exp(1000); print x}'
26881171441816135609425340043592903554686976
$ gawk 'BEGIN{x=exp(1000); print x}'
gawk: warning: exp argument 1000 is out of range
inf
$
```

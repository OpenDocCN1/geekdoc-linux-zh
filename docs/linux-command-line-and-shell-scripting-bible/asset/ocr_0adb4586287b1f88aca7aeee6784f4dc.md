```
> for (i = 1; i < 4; i++)
> (
> total += $1
>
> avg = total / 3
> print "Average:",avg
>)' data5
Average: 128.333
Average: 137.667
Average: 176.667
$
```

By defining the iteration counter in the for loop, you don't have to worry about incrementing yourself like you did when using the while statement.

# Formatted Printing

You may have noticed that the print statement doesn't exactly give you much control over how gawk displays your data. About all you can do is control the output field separator character (OFS). If you're creating detailed reports, you'll need to place data in a specific format and location.

The solution is to use the formatted printing command, called printf. If you're familiar with C programming, the printf command in gawk performs the same way, allowing you to specify detailed instructions on how to display data.

The format of the printf command is:

```
printf "format string", var, var2...
```

The format string is the key to the formatted output. It specifies exactly how the formatted output should appear, using both text elements and specifiers. A format specifier is a special code that indicates what type of variable is displayed and how to display it. The gawk program uses each specifier as a placeholder for each variable listed in the command. The first format specifier matches the first variable listed, the second matches the second variable, and so on.

The format specifiers use the:
%[modifier]control-letter

control-letter is one character code that indicates what type of data value will be displayed, and modifier defines an optional formatting feature.

Table 19-3 lists the control-letters that can be used in the format specifier.
# Table 9.23 Format Specifiers for the printf Command

| Format Specifier | Value |
|---|---|
| \" | Double quote |
| \0NNN | An octal character in which NNN represents 0 to 3 digits |
| \\ | Backslash |
| \a | Alert or beep |
| \b | Backspace |
| \c | Produce no further output |
| \f | Form feed |
| \n | Newline |
| \r | Carriage return |
| \t | Horizontal tab |
| \v | Vertical tab |
| \xNNN | Hexadecimal character in which NNN is 1 to 3 digits |
| %% | Single % |
| %b | ARGUMENT as a string with \ escapes interpreted |

# EXAMPLE 9.103

```
1 > printf --version
printf (GNU sh-utils) 1.16
2 > printf "The number is %.2f\n" 100
The number is 100.00
3 > printf "% -20s%-15s%10.2f\n" "Jody" "Savage" 28
Jody              Savage                28.00
4 > printf "%s-20s%-15s%10.2f\n" "Jody" "Savage" 28
/Jody             /Savage                28.00/
```

# EXPLANATION

+   1 The GNU version of the printf command is printed. It is found in /usr/bin.
+   2 The argument 100 is printed as a floating-point number with only two places to the right of the decimal point printing, designated by the format specification %.2f in the format string. Note that unlike C, there are no commas separating the arguments.
to be written. You can even use this macro in a subsequent macro definition to convert an ASCII character from lowercase to uppercase, leaving any nonlowercase character unchanged:

```
Click here to view code image
#

```

The program loop

```
Click here to view code image
\u\n\u007b\n\u007d

```

would sequence through the characters pointed to by `$`, converting any lowercase characters in the string to uppercase.⁵

> 5. There are a host of functions in the library for doing character tests and conversions. For example, `islower` and `toupper` serve the same purpose as the macros `IS_LOWER_CASE` and `TO_UPPER`. For more details, consult Appendix B, “The Standard C Library.”

# Variable Number of Arguments to Macros

A macro can be defined to take an indeterminate or variable number of arguments. This is specified to the preprocessor by putting three dots at the end of the argument list. The remaining arguments in the list are collectively referenced in the macro definition by the special identifier `__` .
As an example, the following defines a macro called `d` to take a variable number of arguments:

```
Click here to view code image
#

```

Legitimate macro uses would include

```
Click here to view code image
d

```

as well as

```
Click here to view code image
d

```

In the first case, the output would be

D

And in the second case, if i had the value 1 and j the value 2 , the output would be

D

The p call in the first case gets expanded into

```
Click here to view code image
p

```

by the preprocessor, which also concatenates the adjacent character string constants together. So the final p call looks like this:
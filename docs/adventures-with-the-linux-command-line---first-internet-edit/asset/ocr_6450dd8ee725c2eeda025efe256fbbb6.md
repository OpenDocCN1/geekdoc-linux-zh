# RS - Record separator

When reading input, AWK interprets this string as the end of record marker. The default value is a newline.

# FILENAME

If AWK is reading its input from a file specified on the command line, then this variable contains the name of the file.

# FNR - File record number

When reading input from a file specified on the command line, AWK sets this variable to the number of the record read from that file.

# Arrays

Single-dimensional arrays are supported in AWK. Data contained in array elements may be either numbers or strings. Array indexes may also be either strings (for associative arrays) or numbers.

Assigning values to array elements is done like this:

| a[1] = 5 | # Numeric index |
| a("five") = 5 | # String index |

Though AWK only supports single dimension arrays (like bash), it provides a mechanism to simulate multi-dimensional arrays. When assigning an array index, it is possible to use this form to represent more than one dimension:

```
a[j,k] = "foo"
```

When AWK sees this construct, it builds an index consisting of the strings j and k separated by the contents of the built-in variable SUBSEP. By default, SUBSEP is set to "034" (character 34 octal, 28 decimal). This ASCII control code is fairly obscure and unlikely to appear in ordinary text, so it is perfectly safe for use in AWK.

Note that both awk and gawk implement language extensions to support multi-dimensional arrays in a formal way. Consult their respective documentation for details. If a portability is needed, use the method rather than the implementation-

We can delete arrays and array elements this way:

| delete[i] # delete a single element |
| delete a # delete array a |

# Arithmetic and Logical Expressions

AWK supports a pretty complete set of arithmetic and logical operators:
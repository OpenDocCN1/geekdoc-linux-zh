# echo—echoes arguments

```
echo [ argument ] ...
echo [ -n ] [ argument ]
```

echo writes its arguments separated by blanks and terminated by a newline on the standard output.

# System V echo options:

+   \b backspace
+   \c suppress newline
+   \f form feed
+   \n newline
+   \r return
+   \t tab
+   \v vertical tab
+   \\ backslash
+   \0n n is a 1, 2, or 3, octal value

# egrep—searches a file for a pattern using full regular expressions

```
egrep [ -bcHilnsv ] [ -e special-expression ] [ -f filename ]
[ strings ] [ filename ... ]
```

egrep (expression grep) searches files for a pattern of characters and prints all lines that contain that pattern. egrep uses full regular expressions (expressions with string values that use the full set of alphanumeric and special characters) to match the patterns.

# EXAMPLE A.23

+   1 egrep 'Tom|John' datafile
+   2 egrep '^ [A-Z]*' file

# EXPLANATION

+   1 Displays all lines in datafile containing the pattern either Tom or John.
+   2 Displays all lines starting with one or more uppercase letters.

# expr—evaluates arguments as an expression

```
expr arguments
```

The arguments are taken as an expression. After evaluation, the result is written to the standard output. The terms of the expression must be separated by blanks. Characters special to the shell must be escaped. Used in Bourne shell scripts for performing simple arithmetic operations.
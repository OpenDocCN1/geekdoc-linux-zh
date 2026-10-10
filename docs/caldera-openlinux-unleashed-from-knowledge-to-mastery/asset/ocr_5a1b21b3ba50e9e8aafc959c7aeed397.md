786

# PART V

# Backslash Substitution

Backslash substitution is used to insert special characters into a word or prevent other kinds of substitution.

For example,

```
```
set price Price:\n|$4.45|\a| box.
```
```

sets price to

```
```
Price:
$4.45 a box.
```
```

The \n sequence inserts a newline into the word. The backslash before the dollar sign prevents Tcl from interpreting the $4 as a variable substitution. The backslashes before the spaces cause the spaces to be considered as part of the word rather than as word separators.

Tcl understands most of the backslash sequences of ANSI C, as illustrated in Table 33.1.

| Table 33.1 | Tcl Backslash Substitutions | |
| --- | --- | --- |
| Backslash Sequence | Replaced By | |
| \a | Audible bell | |
| \b | Backspace | |
| \f | Form feed | |
| \n | Newline | |
| \r | Carriage return | |
| \t | Tab | |
| \v | Vertical tab | |
| \ddd | Octal value given by ddd | |
| \xhh | Hex value given by hh | |
| \newline | A single space | |

A backslash followed by any character not in Table 33.1 is replaced with the second character. This lets you turn off the special interpretation Tcl normally gives to characters such as $, [, and \.

# Quoting

Tcl provides two other ways besides backslash substitution to prevent the parser from giving special meanings to characters, like $.
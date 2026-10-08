# Variables and Constants

**Variables** are symbolic names that represent values stored in memory. For example, the variable `$x` might hold the value `100`, and `$name` might hold the sequence of characters, "Charlie." The value of a variable can change while the program runs. **Constants**, however, do not change value as the program runs. They are written into the program code itself. For example, this statement assigns the value of the constant `127.89` to the variable `$num`:

```
$num = 127.89
```

# Scalars

In the broadest sense, data is perceived as being either numeric or non-numeric. A non-numeric field of information is treated simply as a string of characters (hence the term *string*). Programmers associate strings with such items as a person's name, address, or license plate number. Numbers can also be used for logical analysis as well as for mathematical computations. A **scalar** is a simple variable that holds a number or a string. Scalar variable names begin with a dollar sign ($).

# Numbers

Numbers are stored inside the computer as either signed integers (as in `14321`) or double-precision floating-point values (as in `23456.85`). Numeric literals (constant values versus variable values) can be either integers or floating-point values. These numeric representations are consistent with all languages, but Perl also uses an additional convention with numeric literals to improve legibility: the underscore character, as in `5_456_678_901`. (Perl uses the comma as a list separator.) The underscore only works within literal numbers specified in a program, not in strings functioning as numbers or in data read from elsewhere. Similarly, hexadecimal constants are expressed with the leading `0x` prefix (as in `0xfff`), and octal constants are expressed with the leading `0` prefix (as in `0256`).

All of these are examples of statements that assign values to numeric scalar variables:

```
$x = 12;
$name = "Jill";
$pay = 12456.89;
```

# Strings

Strings are often used for logical analysis, sorts, or searches. **Strings** are sequences of any types of characters (including numbers that are treated as "characters" rather than digits). String literals are usually delimited by either single quotes (`' '`) or double quotes (`" "`). Single-quoted strings are not subject to interpolation (except for `\'` and `\\`, used to put single quotes and backslashes into a single-quoted string). Double quotes use the backslash (`\`) to precede a character that is to be treated as a control character. Table 9-3 lists the code and meaning for each string representation.

## The substr Function.

The substr function returns the substring of a string starting at a position where the first position is one. If the length of the substring is given, that part of the string is returned. If the specified length exceeds the actual string, the string is returned.

### FORMAT

```
substr(string, starting position)
substr(string, starting position, length of string)
```

### EXAMPLE 6.151

```
% nawk ' { print substr("Santa Claus", 7, 6) } ' filename
Claus
```

### EXPLANATION

In the string Santa Claus, print the substring starting at position 7 with a length of 6 characters.

## The match Function.

The match function returns the index where the regular expression is found in the string, or zero if not found. The match function sets the built-in variable RSTART to the starting position of the substring within the string, and RLENGTH to the number of characters to the end of the substring. These variables can be used with the substr function to extract the pattern. (Works only with nawk.)

### FORMAT

```
match(string, regular expression)
```

### EXAMPLE 6.152

```
% nawk 'END{start=match("Good ole USA", /[A-Z]+$/); print start}'\
filename
10
```

### EXPLANATION

The regular expression /[A-Z]+$/ says search for consecutive uppercase letters at the end of the string. The substring USA is found starting at the tenth character of the string Good ole USA. If the string cannot be matched, 0 is returned.

### EXAMPLE 6.133

```
1 % awk 'END{start=match("Good ole USA", /[A-Z]+S/);\nprint RSTART, RLENGTH}' filename
10 3
2 % awk 'BEGIN{ $line="Good ole USA"; } \
END{ match($line, /[A-Z]+S/);\nprint substr($line, RSTART, RLENGTH)}' filename
USA
```

### EXPLANATION

- 1 The RSTART variable is set by the match function to the starting position of the regular expression matched. The RLENGTH variable is set to the length of the substring.
- 2 The substr function is used to find a substring in the variable $line, and uses the RSTART and RLENGTH values (set by the match function) as the beginning position and length of the substring.

## The split Function.

The split function splits a string into an array using whatever field separator is designated as the third parameter. If the third parameter is not provided, awk will use the current value of FS.

### FORMAT

```
split (string, array, field separator)
split (string, array)
```

### EXAMPLE 6.134

```
% awk 'BEGIN{split("12/25/2001",date,",");print date[2]}' filename
25
```

### EXPLANATION

The split function splits the string 12/25/2001 into an array, called date, using the forward slash as the separator. The array subscript starts at 1. The second element of the date array is printed.

## The sprintf Function.

The sprintf function returns an expression in a specified format. It allows you to apply the format specifications of the printf function.

### FORMAT

```
variable=sprintf("string with format specifiers ", expr1, expr2, ... , expr2)
```

### EXAMPLE 6.15

```
% awk '{line = sprintf ("%-15s %.2f", $1, $3); print line}' filename
```

### EXPLANATION

The first and third fields are formatted according to the printf specifications (a left-justified, 15-space string and a right-justified, 6-character floating-point number). The result is assigned to the user-defined variable line. See 'The printf Function' on page 223.

## 6.22 Built-In Arithmetic Functions

Table 6.13 lists the built-in arithmetic functions, where x and y are arbitrary expressions.

| Function | Value Returned |
|---|---|
| `atan2(x,y)` | Arctangent of y/x in the range |
| `cos(x)` | Cosine of x (x in radians) |
| `exp(x)` | Exponential function e to the power of x |
| `int(x)` | Integer portion of x; truncated toward 0 when x > 0 |
| `log(x)` | Natural (base e) logarithm of x |
| `rand( )` | Random number r, where 0 < r < 1 |
| `sin(x)` | Sine of x (with x in radians) |
| `sqrt(x)` | Square root of x |
| `srand(x)` | x is a new seed for `rand( )` |

### 6.22.1 Integer Function

The int function truncates any digits to the right of the decimal point to create a whole number. There is no rounding off.

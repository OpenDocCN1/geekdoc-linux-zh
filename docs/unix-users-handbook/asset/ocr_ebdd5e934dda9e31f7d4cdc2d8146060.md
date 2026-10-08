where a relcop is any of the six relational operators in C, and a matchop is either ~ (matches) or !~ (does not match). A conditional is an arithmetic expression, a relational expression, or a Boolean combination of the two.

The special patterns BEGIN and END can be used to capture control before the first input line is read and after the last. BEGIN and END do not combine with other patterns.

# Special Characters

The following special escape sequences are recognized by awk in both regular expressions and strings:

| Escape | Meaning |
| :--- | :--- |
| `\a` | alert character |
| `\b` | backspace character |
| `\f` | form-feed character |
| `\n` | new-line character |
| `\r` | carriage-return character |
| `\t` | tab character |
| `\v` | vertical-tab character |
| `\nnn` | 1- to 3-digit octal value nnn |
| `\xhhh` | 1- to n-digit hexadecimal number |

# Variable Names

Variable names with special meanings are:

| Variable | Meaning |
| :--- | :--- |
| FS | Input field separator regular expression; a space character by default; also settable by option -Ffs. |
| NF | The number of fields in the current record. |
| NR | The ordinal number of the current record from the start of input. Inside a BEGIN action the value is zero. Inside an END action the value is the number of the last record processed. |
| FNR | The ordinal number of the current record in the current file. Inside a BEGIN action the value is zero. Inside an END action the value is the number of the last record processed in the last file processed. |
| FILENAME | A pathname of the current input file. |
| RS | The input record separator; a newline character by default. |
| OFS | The print statement output field separator; a space character by default. |
| ORS | The print statement output record separator; a newline character by default. |
| OFMT | Output format for numbers (default %.6g). If the value of OFMT is not a floating-point format specification, the results are unspecified. |
| CONVFMT | Internal conversion format for numbers (default %.6g). If the value of CONVFMT is not a floating-point format specification, the results are unspecified. |
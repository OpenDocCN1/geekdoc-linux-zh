field and the blank lines as record separators.

# Data variables

Besides the field and record separator variables, `gawk` provides some other built-in variables to help you know what's going on with your data and to extract information from the shell environment. Table 22.2 shows the other built-in variables in `gawk`.

| **Variable** | **Description** |
|---|---|
| ARGC | The number of command-line parameters present. |
| ARGIND | The index in ARGV of the current file being processed. |
| ARGV | An array of command-line parameters. |
| CONVFMT | The conversion format for numbers (see the printf statement). The default value is %.6 g . |
| ENVIRON | An associative array of the current shell environment variables and their values. |
| ERRNO | The system error if an error occurs when reading or closing input files. |
| FILENAME | The filename of the data file used for input to the `gawk` program. |
| FNR | The current record number in the data file. |
| IGNORECASE | If set to a non-zero value, ignore the case of characters in strings used in the `gawk` command. |
| NF | The total number of data fields in the data file. |
| NR | The number of input records processed. |
| OFMT | The output format for displaying numbers. The default is %.6g , which displays the value in either floating-point or scientific notation, whichever is shorter, using up to six decimal places. |
| RLENGTH | The length of the substring matched in the match function. |
| RSTART | The start index of the substring matched in the match |

TABLE 22.2 More gawk Built-in Variables
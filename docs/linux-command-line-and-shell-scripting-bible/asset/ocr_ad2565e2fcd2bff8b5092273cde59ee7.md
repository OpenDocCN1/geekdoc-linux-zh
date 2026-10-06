# Advanced gawk

Detroit, MI 48201
(313)555-4938
$ gawk 'BEGIN(FS="\n"; RS="\n") {print $1,$4}' data2
Riley Mullen (312)555-1234
Frank Williams (317)555-9876
Haley Snell (313)555-4938
$

Perfect, the gawk program interpreted each line in the file as a data field and the blank lines as record separators.

# Data variables

Besides the field and record separator variables, gawk provides some other built-in variables to help you know what's going on with your data and extract information from the environment. Table 19-2 shows the other built-in variables in gawk.

TABLE 19-2

# More gawk Built-in Variables

| Variable | Description |
| --- | --- |
| ARGC | The number of command line parameters present. |
| ARGIND | The index in ARGV of the current file being processed. |
| ARGV | An array of command line parameters. |
| CONVFMT | The conversion format for numbers (see the printf statement). The default value is %.g. |
| ENVIRON | An associative array of the shell environment variables and their values. |
| ERRNO | The system error an error occurs when reading or closing input files. |
| FILENAME | The name of the data file used for input to the gawk program. |
| FNR | The current record number in the data file. |
| IGNORECASE | Set to a non-zero value, ignore the case of characters in strings used in the gawk command. |
| NF | The total number of data fields in the data file. |
| NR | The number of input records processed. |
| OFMT | The output format for displaying numbers. The default is %.6g. |
| RLENGTH | The length of the substring matched in the match function. |
| RSTART | The start index of the substring matched in the match function. |

505
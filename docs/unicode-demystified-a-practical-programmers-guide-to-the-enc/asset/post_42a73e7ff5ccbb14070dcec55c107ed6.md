
# 1186 gawk

## Options

- --assign var=value Assigns value to the var. The assignment takes place prior to execution of the gawk program and is available within the BEGIN pattern (see the next section). You can repeat this option as many times as needed.
- --field-separator fs -F fs Uses tabs as the value of the input field separator (FS variable).
- --program -f program Reads its program from the file named program. You can use this option more than once on the command line.
- --help -W help Summarizes how to use gawk.
- --lint -W lint Warns about constructs that may not be correct or ones that may not be portable.
- --posix -W posix Runs a POSIX-compliant version of gawk. This option introduces some restrictions: See the gawk man page for details.
- --traditional -W traditional Ignores the GNU features in a gawk program, making the program conform to UNIX awk.

## Notes

The gawk utility is the GNU version of UNIX awk that is provided with GNU/Linux. For convenience Red Hat Linux systems provide a link from /bin/awk to /bin/gawk so that you can run the program using either name.

See page 1208 for examples of gawk error messages.

## Discussion

A gawk program consists of one or more program lines containing a pattern and/or action in the following format:

```
pattern { action }
```

The pattern selects from the input file. The gawk utility performs the action on all lines that the pattern selects. You must enclose the action within braces so that gawk can differentiate it from the pattern. If a program line does not contain a pattern, gawk selects all lines in the input file. If a program line does not contain an action, gawk copies the selected lines to standard output.

To start, gawk compares the first line in the input file (the file-list) with each pattern in the program-file or program. If a pattern selects the line (if there is a match), gawk takes the action associated with the pattern. If the line is not selected, gawk takes no action. When gawk has completed its comparisons for the first line of the input file, it repeats the process for the next line of input file, continuing this process, comparing subsequent lines in the input file, until it has read the entire file-list.

If several patterns select the same line, gawk takes the actions associated with each of the patterns in the order in which they appear. It is, therefore, possible for gawk to send a single line from the input file to standard output more than once.

## Patterns

You can use a regular expression (Appendix A), enclosed within slashes, as a pattern. The ~ operator tests whether a field or variable matches a regular expression. The != operator tests for no match. You can perform both numeric and string comparisons by using the relational operators listed in Table III-13.

## Actions

| Operator | Description |
| :--- | :--- |
| < | Less than |
| <= | Less than or equal to |
| == | Equal to |
| != | Not equal to |
| >= | Greater than or equal to |
| > | Greater than |

You can combine any of the patterns described above using the Boolean operators || (OR) or && (AND).

The comma is the range operator. If you separate two patterns with a comma, a single gawk program line, gawk selects a range of lines, beginning with the first line that matches the first pattern. The last line gawk selects the next subsequent line that matches the second pattern. After gawk finds the second pattern, it starts the process by looking for the first pattern again.

Two unique patterns, BEGIN and END, execute commands before gawk starts its processing and after it finishes. The gawk utility executes the actions associated with the BEGIN pattern before, and with the END pattern after, it processes all the files in the file-list.

The action portion of a gawk command causes gawk to take action when it matches a pattern. When you do not specify an action, gawk performs the default action, which is the print command (explicitly represented as {print}). This action copies the record (normally a line—see “Variables,” following) from the input file to gawk’s standard output.

You can follow a print command with arguments, causing gawk to print only the arguments you specify. The arguments can be variables or string constants. Using gawk, you can send the output from a print command to a file (>), append it to a file (>>), or pipe it to the input of another program (|).

Unless you separate items in a print command with commas, gawk catenates them. Commas cause gawk to separate the items with the output field separator (normally a SPACE—“Variables,” following).

You can include several actions on one line within a set of braces by separating them with semicolons.

## Comments

The gawk utility disregards anything on a program line following a pound sign (#). You can document a gawk program by preceding comments with this symbol.

## Variables

Variables in gawk are not declared prior to their use. You can optionally give a variable an initial value. Numeric variables that do not initialize are automatically initialized to 0; string variables, to the null string. In addition to user variables, gawk maintains program variables for your use. You can use both user and program variables in the pattern and in the action portion of a gawk program. Table III-14 lists a few of the available program variables.

## Variable

| Variable | Description |
| :--- | :--- |
| $0 | The current record (as a single variable) |
| $1-$n | Fields in the current record |
| FILENAME | Name of the current input file |
| FS | Input field separator (default: SPACE or TAB) |
| NF | Number of fields in the current record |
| NR | Record number of current record |
| OFS | Output field separator (default: SPACE) |
| ORS | Output record separator (default: NEWLINE) |
| RS | Input record separator (default: NEWLINE) |

In addition to initializing variables within your awk program, you can use the -v option to initialize variables on the command line. Initializing variables in this manner can be useful if the value of a variable changes from one run of awk to the next.

The input and output record separators are, by default, NEWLINE characters. awk takes each line in the input file to be a separate record and appends a NEWLINE to the end of each record that it sends to standard output. The input field separators are, by default, SPACES and TABS. The output field separator is a SPACE. You can change the value of any of the separators at any time by assigning a new value to its associated variable. This assignment can be done either within a awk program or on the command line using the -v option.

## Functions

Table III-15 lists a few of the functions that awk provides for manipulating numbers and strings.

| Name | Description |
| :--- | :--- |
| length(str) | Returns the number of characters in str; if you do not supply an argument, it returns the number of characters in the input record |
| int(num) | Returns the integer portion of num |
| index(str1,str2) | Returns the index of str2 in str1 or 0 if str2 is not present |
| split(str,arr,del) | Places elements of str delimited by del, in the arr[1]..arr[n]; returns the number of elements |
| sprintf(fmt,args) | Formats args according to fmt and returns the formatted string; mimics the C language function of the same name |
| substr(str,pos,len) | Returns a substring of str that begins at pos and is len characters long |
| tolower(str) | Returns a copy of str in which all uppercase letters are replaced with their lowercase counterparts |
| toupper(str) | Returns a copy of str in which all uppercase letters are replaced with their uppercase counterparts |

## Operators

The gawk arithmetic operators listed in Table III-16 are from the C programming language.

| Operator | Description |
| :--- | :--- |
| * | Multiplies the expression preceding the operator by the expression following it |
| / | Divides the expression preceding the operator by the expression following it |
| % | Takes the remainder after dividing the expression preceding the operator by the expression following it |
| + | Adds the expression preceding the operator to the expression following it |
| - | Substracts the expression following the operator from the expression preceding it |
| = | Assigns the value of the expression following the operator to the variable preceding it |
| ++ | Increments the variable preceding operator |
| -- | Decrements the variable preceding operator |
| += | Adds the expression following the operator to the variable preceding it and assigns the result to the variable preceding the operator |
| -= | Substracts the expression following the operator from the variable preceding it and assigns the result to the variable preceding the operator |
| *= | Multiplies the variable preceding the operator by the expression following it and assigns the result to the variable preceding the operator |
| /= | Divides the variable preceding the operator by the expression following it and assigns the result to the variable preceding the operator |
| %= | Takes the remainder, after dividing the variable preceding the operator by the expression following it, and assigns the result to the variable preceding the operator |

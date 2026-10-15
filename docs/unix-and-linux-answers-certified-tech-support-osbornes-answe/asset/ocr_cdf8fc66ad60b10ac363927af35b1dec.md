# OPTIONS AND VARIABLES

+   -b Ignore repeating blanks and end-of-line blanks.
+   -e Generate a script for the editor ed.
+   -f Produce a script to re-create file1 from file2.

# echo -n string

# OBJECTIVE:

Writes the string to standard output. By default, echo follows all output with a newline. -n suppresses this. The special escape characters, preceded by \, will produce special output sequences:

| Character | Meaning |
| --- | --- |
| \b | Backspace |
| \c | Don't print a newline at the end (same as -n) |
| \f | Form feed |
| \n | Newline |
| \r | Carriage return |
| \t | Tab character |
| \\ | Backslash |

# fg [jobIDs]

# OBJECTIVE:

Put current job or specified jobIDs in the foreground.

# find pathname condition

# OBJECTIVE:

Searches the specified directories generating a list of files that match the criteria specified.

# OPTIONS AND VARIABLES

+   -name file Matches the specified file. If enclosed in quotation marks ("). file can contain wildcards * and ?.
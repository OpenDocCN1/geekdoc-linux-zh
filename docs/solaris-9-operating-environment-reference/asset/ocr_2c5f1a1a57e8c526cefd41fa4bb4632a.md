# cat 121

The following syntax concatenates file1 and file2 and writes the results into
file3. If you give no input file, cat reads from the standard input file.
cat file1 file2 >file3

The following syntax appends the contents of file1 to the end of file2.
cat file1 >> file2

The following syntax displays the contents of file1, file2, and file3 in sequence
y terminal.

> Note — Redirecting the output of cat onto one of the files being read
overwrites the data originally in the file without any warning message.

# Options

+   -n Precede each line output with its line number.
-b Number the lines, as with -n, but omit the line numbers from blank
lines.
-s Be silent about nonexistent files.
-u Do not buffer the output. (The default is buffered output.)
-v Display nonprinting characters (with the exception of Tabs, newlines,
and feeds). ASCII control characters (octal 000–037) are printed as
^n, where n is the corresponding ASCII character in the range octal
100–137 (@ A, B, C, ..., X, Y, Z, [, \], ^, and _); the DEL character
(octal 0177) is printed ?. Other nonprintable characters are printed as
M-x where x is the ASCII character specified by the low-order seven
bits.

You can combine the following options with the -v option.

+   -e Print a $ character at the end of each line (before the newline).
-t Print Tabs as ^I and feeds as ^L.

-e and -t options are ignored if you do not specify the -v option.

# Operands

+   file A path name of an input file. If no file is specified, use the standard
input. If file is -, read from the standard input at that point in the
sequence. cat does not close and reopen standard input when it is
referenced in this way but accepts multiple occurrences of dash (-) as
file.

# Usage

See largefile(5) for the description of the behavior of cat when encountering files
gre than or equal to 2 Gbytes(**33 bytes).
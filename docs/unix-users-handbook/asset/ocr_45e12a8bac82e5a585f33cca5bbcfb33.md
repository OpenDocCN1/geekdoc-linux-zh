# cmp

![](bbox=[0.03, 0.12, 0.13, 0.22])

# cmp - Compare files.

cmp(1)

# NAME

cmp - compare two files

# SYNOPSIS

```
cmp [-l] [-s] file1 file2
```

# DESCRIPTION

cmp compares two files (if file1 or file2 is -, the standard input is used). Under default options, cmp makes no comment if the files are the same; if they differ, it announces the byte and line number at which the difference occurred. If one file is an initial subsequence of the other, that fact is noted.

cmp recognizes the following options:

+           -l              Print the byte number (decimal) and the differing bytes (octal) for each difference (byte numbering begins at 1 rather than 0).

+           -s              Print nothing for differing files; return codes only.

# EXTERNAL INFLUENCES

Environment Variables

LANG determines the language in which messages are displayed. If LANG is not specified or is set to the empty string, a default of "C" (see lang(5)) is used instead of LANG. If any internationalization variable contains an invalid setting, cmp behaves as if all internationalization variables are set to "C". See environ(5).

International Code Set Support

Single- and multi-byte character code sets are supported.

# DIAGNOSTICS

cmp returns the following exit values:

+           0               Files are identical.

+           1               Files are not identical.

+           2               Inaccessible or missing argument.

cmp prints the following warning if the comparison succeeds till the end of file of file1(file2) is reached.

cmp: EOF on file1(file2)

# SEE ALSO

comm(1), diff(1).

# STANDARDS CONFORMANCE

cmp: SVID2, SVID3, XPG2, XPG3, XPG4, POSIX.2
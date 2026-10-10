A whitespace separated list of field widths. When set, gawk parses the input into fields of fixed width, instead of using the value of the FS variable as the field separator. See Fields, above.

# FILENAME

The name of the current input file. If no files are specified on the command line, the value of FILENAME is "-". However, FILENAME is undefined inside the BEGIN rule (unless set by getline).

# FNR

The input record number in the current input file.

# FPAT

A regular expression describing the contents of the fields in a record. When set, gawk parses the input into fields, where the fields match the regular expression, instead of using the value of the FS variable as the field separator. See Fields, above.

# FS

The input field separator, a space by default. See Fields, above.

# FUNCTAB

An array whose indices and corresponding values are the names of all the user-defined or extension functions in the program. NOTE: You may not use the delete statement with the FUNCTAB array.

# IGNORECASE

Controls the case-sensitivity of all regular expression and string operations. If IGNORECASE has a non-zero value, then string comparisons and pattern matching in rules, field splitting with FS and FPAT, record separating with RS, regular expression matching with ~ and !~, and the gensub(), gsub(), index(), match(), patsplit(), split(), and sub() built-in functions all ignore case when doing regular expression operations. NOTE: Array subscripting is not affected. However, the asort() and asorti() functions are affected.

Thus, if IGNORECASE is not equal to zero, /aB/ matches all of the strings ab, aB, Ab, and AB. As with all Awk variables, the initial value of IGNORECASE is zero, so all regular expression and string operations are normally case-sensitive.

# LINT

Provides dynamic control of the --lint option from within an Awk program. When true, gawk prints lint warnings. When false, it does not. When assigned the string value fatal, lint warnings become fatal errors, exactly like --lint=fatal. Any other true value just prints warnings.

# NF

The number of fields in the current input record.

# NR

The total number of input records seen so far.

# OFMT

The output format for numbers, %.6g, by default.

# OFS

The output field separator, a space by default.
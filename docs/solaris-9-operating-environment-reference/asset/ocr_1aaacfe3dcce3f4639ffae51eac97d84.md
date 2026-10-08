# 892

# nawk

The nawk command interprets each record as a sequence of fields where, by default, a field is a string of nonblank characters. You can change this default white-space field delimiter (blanks and/or tabs) by using the FS built-variable or -F ERE option. The awk command denotes the first field in a record as $1, the second $2, and so forth. The symbol $0 refers to the entire record; setting any other field reevaluates it. Assigning to $0 resets the values of all fields and the NF built-in variable.

nawk is a new version of awk that provides capabilities unavailable in previous versions. This version becomes the default version of awk in the next major release.

Input white space is not preserved on output if fields are involved. There are no explicit conversions between numbers and strings. To force an expression to be treated as a number, add 0 to it; to force it to be treated as a string, concatenate the null string ("*") to it.

# Options

+   -F ERE

Define the input field separator to the extended regular expression ERE, before any input is read (can be a character).

+   -f profofile

Specify the path name of the file profofile containing a nawk program. If you specify multiple instances of it, process the concatenation of the files in the order specified in profofile. Alternatively, you can specify the nawk program in the command line as a single argument.

+   -v assignment

The assignment argument must be in the same form as an assignment operand. The assignment is of the form var=value, where var is the name of one of the variables described below. The specified assignment occurs before nawk program is executed including the actions associated with BEGIN patterns (if any). You can specify this option multiple times.

# Operands

+   program

If you specify -f option, the first operand to nawk is the text of the nawk program. The application supplies the program operand as a single argument. If the text does not end in a newline character, nawk interprets the text as it fit did.

+   argument

You can intermix either of the following two types of arguments.

+   file

A path name of a file that contains the input to be read, which is matched against the set of patterns in the program. If you specify no file operands or if a file operand is -, use the standard input.
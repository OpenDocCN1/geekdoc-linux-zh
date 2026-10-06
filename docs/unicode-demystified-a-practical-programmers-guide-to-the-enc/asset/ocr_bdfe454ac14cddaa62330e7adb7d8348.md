# 1186 gawk

# Options

--assign var=value var= Assigns value to the var. The assignment takes place prior to execution of the gawk program and is available within the BEGIN pattern (see the next section). You can repeat this option as many times as needed.

--field-separator fs -F fs Uses ts as the value of the input field separator (FS variable).

--program -f program Reads its program from the file named program. You can use this option more than once on the command line.

--help -W help Summarizes how to use gawk.

--lint -W lint Warns about constructs that may not be correct or ones that may not be portable.

--posix -W posix Runs a POSIX-compliant version of gawk. This option introduces some restrictions: See the gawk man page for details.

--traditional -W traditional Ignores the GNU features in a gawk program, making the program conform to UNIX awk.

# Notes

The gawk utility is the GNU version of UNIX awk that is provided with GNU/Linux. For convenience Red Hat Linux systems provide a link from /bin/awk to /bin/gawk so that you can run the program using either name.

See page 1208 for examples of gawk error messages.

# Discussion

A gawk program consists of one or more program lines containing a pattern and/or action in the following format:

```
pattern { action }
```

The pattern selects from the input file. The gawk utility performs the action on all lines that the pattern selects. You must enclose the action within braces so that gawk can differentiate it from the pattern. If a program line does not contain a pattern, gawk selects all lines in the input file. If a program line does not contain an action, gawk copies the selected lines to standard output.

To start, gawk compares the first line in the input file (the file-list) with each pattern in the program-file or program. If a pattern selects the line (if there is a match), gawk takes the action associated with the pattern. If the line is not selected, gawk takes no action. When gawk has completed its comparisons for the first line of the input file, it repeats the process for the next line of input file, continuing this process, comparing subsequent lines in the input file, until it has read the entire file-list.
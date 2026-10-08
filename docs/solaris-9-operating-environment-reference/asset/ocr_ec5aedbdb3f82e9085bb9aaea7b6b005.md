# 920

# newform

# See Also

newform(1), sendmail(LM), aliases(4), attributes(5)

# newform — Change the Format of a Text File

# Synopsis

```
/usr/bin/newform -s -itabspec -otabspec [-bn] [-en] [-pn] [-an] [-f] -cchar -ln [filename...]
```

# Description

The newform command to reformat files according to the specified options, newform reads lines from the named file, or the standard input if you specify no input file, and reproduces the lines on the standard output. Lines are reformatted in accordance with the specified command-options.

Except for -s, you can specify options in any order, repeat them, and interming with their optimal file names. Command-line options are processed in the order specified. This means that sequences such as -e15 -160 yields different results from -160 -e15. Options are applied to all file names on the command line.

# Notes

newform normally tracks only of physical characters; however, for the -i and -o options, newform keeps track of backspaces to be able to line up Tabs in the appropriate columns.

newform does not prompt you if a tabspec is to be read from the standard input (by use of -i-- or -o--).

If you use the -f option and the last -o option specified -o-- and it was preceded by either a -o-- or a -i---, the Tab specification format line is correct.

# Options

+   -an Same as -pn, except append characters to the end of a line.

+   -bn Truncate n characters from the beginning of the line when the line length is greater than the effective length (see -ln). Default is to truncate the number of characters necessary to obtain the effective line length. The default value is used when you specify -b with no n. You can use this option to delete the sequence numbers from a COBOL program as follows: newform -ln1 -b7 filename

+   -cchar Change the prefix/append character to char. Default character for char is a space.

+   -en Same as -bn, except truncate characters from the end of the line.

+   -f Write the Tab specification format line on the standard output before any other lines are output. The Tab specification format line that is printed corresponds to the format specified in the last -o option. If you specify no -o, the line that is printed contains the default specification of -8.
# 1150 diff

--ignore-blank-lines -B Ignores differences that involve only numbers of blank lines.

--ignore-case -i Ignores differences in case when comparing files.

--ignore-space-change -b Ignores blanks (SPACES AND TABS) at the ends of lines and considers others strings of blanks equal.

--p Shows which function each change is in.

--recursive -r When using diff to compare the files in two directories, causes the comparisons to extend through subdirectories as well.

--side-by-side -y Displays output in a side-by-side format. This option generates the same output as sdiff. Use the --width=columns option with this option.

--unified[lines=n] -u Uses the easier-to-read unified output format. See the discussion of diff on page 67 for more detail and an example. The lines are the number of lines of context; the default is three.

-w whitespace Ignores whitespace when comparing files.

--width=columns -w Sets the number of columns that diff uses to display the output columns. This option is useful with the --side-by-side option. The sdiff utility uses lowercase w to perform the same function: -w columns.

# Notes

The diff utility is similar to sdiff, but the output may be easier to read. The --side-by-side option to diff produces the same output as sdiff. If you experiment with sdiff, make sure that you use the -w columns option, which sets the page width to columns characters (the default is 130). See the "Examples" section and refer to the diff and diff into pages for more information.

# Discussion

When you use diff without any options, it produces a series of lines Adding (a), Delete (d), and Change (c) instructions. Each of these lines is followed by the lines from the file that you need to add, delete, or change. A less symbol (<) precedes lines from file1. A greater than symbol (>) precedes lines from file2. The diff output is in the format shown III-10. A pair of lines separated by a comma represents a range of lines; diff uses a single line number to represent a single line.
```
<Ctrl+D>
$ ed Fall_OH < diff.script
209
177
$ diff Fall_OH Spring_OH
$
```

Most systems have a command called diff3 that can be used to do a three-way comparison; that is, three files can be composed.

# 6.7 LOCATING AND REMOVING REPETITION WITHIN TEXT FILES

You can use the uniq command to remove all but one copy of the successive repeated lines in a file. The command is intended for files of sorted content although it can work on files without sorted content, as shown in the example. We discuss sorting in Chapter 7. The following is a brief summary of the command.

```
SYNTAX
uniq [options] [input-file] [output-file]

Purpose: Remove repetitious lines from the sorted input-file and send unique (nonrepeated) lines to output-file. The input-file does not change. If no output-file is specified, the output of the command is sent to standard output. If no input-file is specified, the command takes input from standard input.

Commonly used options/features:
-c  Precede each output line by the number of times it occurs
-d  Display the repeated lines
-f N Ignore the first N fields in input lines while doing comparisons
-i  Perform case-sensitive comparison of input lines
-s C Ignore the first C characters in input lines while doing comparisons
-u  Display the lines that are not repeated
```

The following session illustrates how the uniq command works. The cat command is used to show the contents of the sample file. The uniq sample command shows that only consecutive duplicate lines are considered duplicate. The uniq -c sample command shows the line count for every line in the file. The uniq -d sample command is used to output repeated lines only. Finally, the uniq -d sample out command sends the output of the command to the out file. The cat out command is used to show the contents of out. Note that the uniq command only works for unsorted files if repeated lines are adjacent.

```
$ cat sample
This is a test file for the uniq command.
It contains some repeated and some nonrepeated lines.
Some of the repeated lines are consecutive, like this.
Some of the repeated lines are consecutive, like this.
```
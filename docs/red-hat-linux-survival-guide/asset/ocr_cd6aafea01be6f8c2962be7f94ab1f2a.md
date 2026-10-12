# diff

Syntax: diff [-iqb] file1 file2

You use the diff command to determine differences between files and/or directories. The diff command is different from the cmp command in the way it compares the files. The diff command is used to report differences between two files, line by line. The cmp command reports differences between two files character by character, instead of line by line. As a result, it is more useful than diff for comparing binary files. By default, diff does not produce any output if the files are identical.

For text files, cmp is useful mainly when you want to know only whether two files are identical.

To illustrate the difference between considering changes character by character and considering them line by line, think of what happens if you add a single newline character to the beginning of a file. If you compare that file with an otherwise identical file that lacks the newline at the beginning, diff reports that a blank line has been added to the file, and cmp reports that the two files differ in almost every character.

The normal output format consists of one or more hunks of differences; each hunk shows one area where the files differ. Normal format hunks look like this:

```
change-command
< from-file-line
< from-file-line. . .
--
> to-file-line
> to-file-line. . .
```

There are three types of change commands. Each consists of a line number or comma-separated range of lines in the first file, a single character indicating the kind of change to make, and a line number or comma-separated range of lines in the second file. All line numbers are the original line numbers in each file. The types of change commands are:

+   - ‘lar’ — Add the lines in range r of the second file after line l of the first file. For example, ‘8a12,15’ means append lines 12–15 of file 2 after line 8 of file 1; or, if changing file 2 into file 1, delete lines 12–15 of file 2.
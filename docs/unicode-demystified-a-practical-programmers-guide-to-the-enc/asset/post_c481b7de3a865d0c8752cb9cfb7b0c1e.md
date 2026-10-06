
$ cat months
Jan
Feb
Mar
Apr
May
Jun
Jul
Aug
Sep
Oct
Nov
Dec

$ head months
Jan
Feb
Mar
Apr
May
Jun
Jul
Aug
Sep
Oct

# **Figure 3-4** head displays the first lines of a file

enclose the string you are searching for in single quotation marks, but doing so allows to use SPACES and special characters in the search string.

The grep utility can do much more than search for a simple string in a single file. Refer to grep on page 1215 in Part III and Appendix A, Regular Expressions, for more information.

## head: Displays the Beginning of the File

The head utility displays the first ten lines of a file. You can use head to help you remember what a particular file contains. If you have a file named months that lists the 12 months of the year in order, one to a line, head displays Jan through Oct (Figure 3-4).

The head utility can display any number of lines, so you can use it to look at only the first line of a file or at a screen or more. To specify the number of lines head displays, include a hyphen followed by the number of lines in the head command. For example, the following command displays only the first line of months:

```
$ head -1 months
Jan
```

The head utility can also display parts of a file based on a count of blocks or characters rather than lines. Refer to page 1222 in Part III for more information on head.

## tail: Displays the End of a File

The tail utility is similar to head but by default displays the last ten lines of a file. Depending on how you invoke it, the tail utility can display fewer or more ten lines, use a count of blocks or characters rather than lines to display parts of a file, and display lines being added to a file that is changing. The following command causes tail to display the last five lines, Aug through Dec, of the months file shown in Figure 3-4:

```
$ tail -5 months
Aug
Sep
Oct
Nov
Dec
```

The ability to display lines as they are added to the end of a file is a useful feature. You can monitor lines as they are added to the end of the growing file logfile with the command

```
$ tail -f logfile
```

Press the interrupt key (usually CTRL-C) to stop tail and return to the shell prompt. Refer to page 1340 in Part III for more information on tail.

## sort: Displays a File in Order

The sort utility displays the contents of a file in order by lines but does not change the original file. If you have a file named days that contains the name of each day of the week on a separate line, sort displays the file in alphabetical order (Figure 3-5).

The sort utility is useful for putting lists in order. The -u option generates a sorted list in which each line is unique (no duplicates). The -n option puts a list of numbers in order. Refer to page 1326 in Part III for more information on sort.

## uniq: Removes Duplicate Lines from a File

The uniq (unique) utility displays a file, skipping adjacent duplicate lines but does not change the original file. If a file contains a list of names and has two successive entries for the same person, uniq skips the extra line (Figure 3-6).

```
$ cat days
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
Sunday
$ sort days
Friday
Monday
Saturday
Sunday
Thursday
Tuesday
Wednesday
```

# **Figure 3-5** sort displays a file in order

If a file is sorted before it is processed by uniq, uniq ensures that no two lines in the file are the same. (Of course, sort can do all by itself with the -u option.)
Refer to page 1368 in Part III for more information on uniq.

## diff: Compares Two Files

The diff (difference) utility compares two files and displays a list of the differences between them. This utility does not change either file and is useful when you want to compare two versions of a letter or report or two versions of the source code for a program.

```
$ cat dups
Cathy
Fred
Joe
John
Mary
Mary
Paula
$ uniq dups
Cathy
Fred
Joe
John
Mary
Paula
```

# **Figure 3-6** uniq removes duplicate lines

## Chapter 3 Introduction to the GNU/Linux Utilities

```
$ diff -u colors.1 colors.2
-- colors.1 Fri Nov 21 15:45:32 2003
+++ colors.2 Fri Nov 21 15:24:46 2003
@@ -1,6 +1,5 @@
red
+blue
+green
+yellow
-pink
+purple
+orange
```

# **Figure 3-7** diff displaying the unified output format

The diff utility with the -u (unified output format, displays two lines indicating which of the files you are comparing will be denoted by a plus sign (+) and by which a minus sign (-). Figure 3-7 shows that a minus sign indicates the colors.1 file; a plus sign, the colors.2 file.
The diff -u command breaks long, multiline text into hunks. Each hunk is preceded by a line number and two at signs (@@). This hunk identifier indicates the starting line number and the number of lines from each file for this hunk. In Figure 3-7 line indicates that the hunk covers the section of colors.1 file (indicated by a minus sign) and continuing from the first line and for six lines (for a total of seven lines). Similarly, the +1,5 indicates that the hunk also covers colors.2 from the first line through five subsequent lines.
Following these header lines, diff -u displays each line of text with a minus sign, plus sign, or nothing. The leading minus sign indicates that the line occurs only in the file denoted by the minus sign. The leading plus sign indicates that the line is from the file denoted by the plus sign. A line that begins with neither a plus nor minus sign occurs in both files in the same location. Refer to page 1149 in Part III for more information on diff.

## file: Tests the Contents of a File

You can use the file utility to learn the contents of any file on a GNU/Linux system without having to open and examine the file yourself. In the following example file letter_e.gz contains data that has been compressed in a particular way:

```
$ file letter_e.gz
letter_e.gz: gzip compressed data, deflated, original filename, last modified: Tue Oct 8 16:02:25 2002, os: Unix
```

Refer to page 1163 in Part III for more information on file.

## I (Pipe): Communicates between Processes

Because pipes are integral to the functioning of a GNU/Linux system they are introduced here for use in examples, Pipes are covered in detail in on page 151.

A process is either the means by which GNU/Linux executes a utility or other program or the utility/program as GNU/Linux executes it (page 142). Communication between processes is one of the hallmarks of UNIX/Linux. A pipe (written as a vertical bar, |, on the command line and appearing as a solid or broken vertical line on keyboards) provides the simplest form of this communication. Simply put, a pipe takes the output of one utility and sends that output as input to another utility. Using UNIX/Linux terminology, a pipe takes standard output of one process and redirects it to become standard input of another process. Most of what a process displays on your screen is sent to standard output. Without being redirected, using a pipe you can redirect that it does not go to the screen but goes instead to standard input of another utility. (See page 142 for more information on standard input and output.)

## Four More Utilities

The echo and date utilities are two of the most frequently used from the large collection of GNU/Linux utilities. The script utility helps you record part of a session, and mcopy makes a copy of a text file that can be read on an Windows machine.

```
$ ls
memo.0714 practice
$ echo Hi
Hi
$ echo This is a sentence.
This is a sentence.
$ echo star: *
star: memo.0714 practice
$ 
```

# **Figure 3-8** echo copies the command line (but not the word echo) to the screen

## echo: Displays Text

The echo utility copies anything you put on the command line after echo to the screen. Some examples are shown in Figure 3-8. The last example shows what the shell does with an unquoted asterisk (*) on the command line: expands into a list of filenames in the directory.

The echo utility is a good tool for learning about the shell and other GNU/Linux programs. Some examples on page 158 use echo to illustrate how special characters, such as the asterisk, work. Throughout Chapters 12–15 echo helps explain shell variables and how to send messages from shell scripts to the screen.

## date: Displays the Time and Date

The date utility displays the current date and time. An example of date is

```
$ date
Wed Mar 13 08:00:38 PST 2002
```

You can choose the format and select the contents of the output of date as in the following example. Refer to page 1441 in Part III for more information on date.

```
$ date +"%A %B %d"
Wednesday March 13
```

## script: Records a GNU/Linux Session

The script utility records all or part of a login session, including your input and the system's responses. This utility is useful only from character-based devices, such as a terminal or a terminal emulator. The utility captures a session with vi, because we uses control characters to position the cursor and display different

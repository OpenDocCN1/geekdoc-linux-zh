(initial, middle, or last part of the file), and whether the file's contents are displayed one screen or one page at a time. Recall that you can view only those files for which you have the read permission. In addition, you must have the execute (search) permissions for all the directories involved in the pathname of the file to be displayed. Viewing does not mean edit, write, or update—just view.

# 6.2.1 Viewing Complete Files

You can display the complete contents of one or more files on screen by using the cat command. However, because the command does not display file contents one screen or one page at a time, you see only the last page of a file that is larger than one page (i.e., one screen) in size. The following is a brief description of the cat command.

```
SYNTAX
cat [options] [file-list]

Purpose: Concatenate/display the files in file-list on standard output (screen by default), one after another
Output: Contents of the files in file-list displayed on the screen, one file at a time
Commonly used options/features:
-e Display $ at the end of each line; works in conjunction with the -v option
-n Put line numbers with the displayed lines
-t Display tabs as ^I and form feeds as ^L
-v Display nonprintable characters, except for the tab, form feed, and newline characters
```

Here, file-list is an optional argument that consists of the pathnames for one or more files, separated by spaces. For example, the following command displays the contents of the student_records file in the present working directory. If the file is larger than one page, the file contents quickly scroll off the display screen.

```
% cat student_records
Jonh Doe ECE 3.54
Pam Meyer CS 3.61
Jim DAVIS CS 2.71
Jason Kim ECE 3.97
Amy Nash ECE 2.38
%
```

The following command displays the contents of files lab1 and lab2 in the directory ~/courses/ee446/labs. The command does not pause after displaying the contents of lab1.

```
$ cat ~/courses/ee446/labs/lab1 ~/courses/ee446/labs/lab2
[ contents of lab1 and lab2 ]
$
```
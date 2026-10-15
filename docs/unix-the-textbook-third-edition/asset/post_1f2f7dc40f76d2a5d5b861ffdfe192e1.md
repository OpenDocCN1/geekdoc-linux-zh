
## SYNTAX

```
cat [file-list] > destination-file
```

Purpose: Put the contents of the files in file-list, in the order specified in the command line, and put them in destination-file

The destination-file is overwritten if it already exists. If you do not have the write permission for the destination-file, the command displays an error message informing you that you do not have permission to write to the file. Without the optional file-list argument, you can use the command to put keyboard input in destination-file. Thus, this command syntax can be used to create a new file whose contents are what you enter from the keyboard until you press <Ctrl+D> on a new line, as is the case with the cat >> test.letter command in the previous session.

The following session illustrates how this command works with arguments. The ls -l command is used to view permissions for the files. The wc memo? command displays the sizes of all the files in the current directory that start with the string memo and have one or more letters after this string. The third command combines the contents of the memo1, memo2, and memo3 files and puts them in the memos.y2k14 file in the order they appear in the command. The wc memos.y2k14 command is used to confirm that the memos.y2k14 file has the same number of lines, words, and characters as the three memo files combined. Execution of the cat memo1 memo2 memo3 > memos.2014 command shows that you do not have permission to write to memos.2014.

```
% ls -l
-rwxr--r-- 1 sarwar faculty 1687 Jan 10 19:15 memo1
-rwxr--r-- 1 sarwar faculty 1227 Feb 19 14:37 memo2
-rwxr--r-- 1 sarwar faculty 790 Sep 1 19:16 memo3
-r-------- 1 sarwar faculty 9765 Jan 15 22:11 memos.2014
% wc memo?
 44 250 3352 memo1
 34 244 4083 memo2
 12 112 907 memo3
 90 606 3704 total
% cat memo1 memo2 memo3 > memos.y2k14
% wc memos.y2k14
 90 606 3704 memos.y2k14
% cat memo1 memo2 memo3 > memos.2014
memos.2014: Permission denied.
%
```

You can also do the task of the cat memo1 memo2 memo3 > memos.y2k14 by using the following command sequence.

```
$ cat memo1 > memos.y2k14
$ cat memo2 >> memos.y2k14
```

```
$ cat memo3 >> memos.y2k14
$
```

The following in-chapter exercises ask you to practice using the cp, mv, ls -l, wc, and cat commands and the operator for appending to a file.

## EXERCISE 6.5

Copy the .profile (or .login in a BSD UNIX-based system) file in your home directory to a file .profile.old (or .login.old) in a directory called backups, also in your home directory. Assume that you are in your home directory. What command did you use?

## EXERCISE 6.6

Create a directory called new.backups in your home directory and move all the files in the backups directory to new.backups. What commands did you use?

## EXERCISE 6.7

Display the size in bytes of a file lab3 in the ~/ece345 directory. What command did you use?

## EXERCISE 6.8

Give a command for appending all the files in the ~/courses/ece446 directory to a file called BigBackup.ece446 in the ~/courses directory.

## 6.6 COMPARING FILES

At times, you will need to compare two versions of a program code or some other document to find out where they differ from each other. You can use the diff command to perform this task. The command compares two files and displays differences between them in terms of commands that can be used to convert one file to the other. The following is a brief description of the command.

## SYNTAX

```
diff [options] [file1] [file2]
```

Purpose: Compare file1 with file2 line by line and display differences between them as a series of commands/instructions for the ed editor that can be used to convert file1 to file2 or vice versa; read from standard input if – is used for file1 or file2

Commonly used options/features:

- -b Ignore trailing (at the end of lines) white spaces (blanks and tabs), and consider other strings of white spaces equal
- -e Generate and display a script for the ed editor that can be executed to change file1 to file2
- -h Do fast comparison (the -e option may not be used in this case)

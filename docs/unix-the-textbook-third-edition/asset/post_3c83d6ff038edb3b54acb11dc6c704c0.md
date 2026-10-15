
+   a. cd dir1
+   b. ls
+   c. rm dir1/mypasswd
+   d. cp /etc/passwd dir1

14. What umask command should be executed to set the permissions bit mask to 037? With this mask, what default access privileges are associated with any new file that you create on the system? Why? Where would you put this command so that every time you log on to the system this mask is effective?

15. Give a command line for setting the default access mode so that you have read, write, and execute privileges, your group has read and execute permissions, and all others have no permission for a newly created executable file or directory. How would you test it to be sure that it works correctly?

16. Give chmod command lines that perform the same tasks as the mesg n and mesg y commands. (Hint: Every hardware device, including your terminal, has an associated file in the /dev directory.)

17. What are the purposes of the set-user-ID (SUID), set-group-ID (SGID), and sticky bits?

18. Give one command line for setting all three special access bits (SUID, SGID, and sticky) for the file cp.new. (Hint: Use octal mode.)

19. In a UNIX system, the cat command is owned by root and has its SUID bit set. Do you see any problems with this setup? Explain your answer.

20. Some UNIX systems do not allow users to change their passwords with the passwd command. How is this restriction enforced? Is it a good or bad practice? Why?

+   f. chmod +t ~/dir1
+   g. chmod ugo-r ~/prog1
+   h. chmod a-rw ~/prog1
+   i. chmod ug+x ~/dir1
+   j. chmod go= ~/dir1
+   k. chmod u=rwx ~/prog1
+   l. chmod g=o ~/dir1
+   m. chmod o=wx ~/dir1

## Basic File Processing

### Objectives

- To discuss how to display contents of a file
- To explain copying, appending, moving/renaming, and removing/deleting files
- To describe how to determine the size of a file
- To discuss commands for comparing files
- To describe how to combine files
- To discuss printer control commands
- To cover the commands and primitives

```
> , >> , ^ , [ ] , * , ? , cancel, cat, cp, diff, head, lp, lpc, lpq, lpr, lprm, lpstat, lptest, less, ls, more, mv, nl, pg, pr, rm, tail, uniq, wc
```

## 6.1 INTRODUCTION

This chapter describes how some basic file operations can be performed in UNIX. These operations are primarily for nondirectory files, although some are applicable to directories as well; we previously discussed the most commonly used directory operations in Chapter 4. When discussing the file operations in this chapter, we also describe related commands and give examples to illustrate how these commands can be used to perform the needed operations. Remember, complete information on a particular command is available via the man command.

## 6.2 VIEWING CONTENTS OF TEXT FILES

You view files to identify their contents. You can use several UNIX commands to display contents of text files on the display screen. These commands differ from each other in terms of the amount of the file content displayed, the portion of file contents displayed

(initial, middle, or last part of the file), and whether the file's contents are displayed one screen or one page at a time. Recall that you can view only those files for which you have the read permission. In addition, you must have the execute (search) permissions for all the directories involved in the pathname of the file to be displayed. Viewing does not mean edit, write, or update—just view.

### 6.2.1 Viewing Complete Files

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
John Doe ECE 3.54
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

RETURN to execute the modified command (it does not matter where the cursor is on the command line).

You can also repeat the previous command using !!. This technique is useful if you forgot to use `su` [page 42.5] to prefix a command. In this case, if you type `su -c "!!"`, the shell will run the previous command with `root` privileges. Or, if the local system is set up to use `sudo` (page 428), you can type `sudo !!` and the shell will run the previous command with `root` privileges.

The command `^old^new^` reruns the previous command, substituting the first occurrence of the string `old` with `new`. Also, on a command line, the shell replaces the characters `!$` with the last token (word) on the previous command line. The following example shows the user correcting the filename `memo` to `memo` using `^n^m^` and then printing the file named `memo` by giving the command `lpr !$`. The shell replaces `!$` with `memo`, the last token on the previous command line.

```
$ cat memo
cat: memo: No such file or directory
$ ^n^m$
cat memo
This is the memo file.
$ lpr !$
lpr memo
```

For information about more complex command-line editing, see page 378.

# RUNNING BASIC COMMAND-LINE UTILITIES

This section describes a few basic command-line utilities. You can experiment with these utilities from a terminal, a terminal emulator within a GUI [page 120], or a virtual console [page 121]. See Chapter 7 for more complete coverage of these and other utilities.

# ls: LISTS THE NAMES OF FILES

Using the editor of your choice, create a small file named `practice`. (See the tutorials on the `vim` [page 262] and `nano` [page 270] editors.) After exiting from the editor, you can use the `ls` (list; page 221) utility to display a list of filenames. Following, `ls` lists the name of the `practice` file. (On the system you are using it might list run some files the system or a program created.)

```
$ ls
practice
```

By default, `ls` lists the names of most of the files in the working directory (the directory you are working in). You can list the names of specified files by providing their names as arguments on the command line. Put a SPACE between the name of the utility and any arguments.

```
$ ls practice
practice
```
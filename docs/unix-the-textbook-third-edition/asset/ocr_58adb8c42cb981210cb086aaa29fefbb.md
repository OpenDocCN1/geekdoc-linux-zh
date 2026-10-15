The shell metacharacters allow you to specify multiple files in multiple directories in one command line. We describe the use of these characters in subsequent chapters, but we give some simple examples here to explain the meanings of some commonly used metacharacters:

+   - *
+   - ?
+   - ~
+   - [ ]

The ?.txt string can be used for all the files that have a single character before .txt, such as a.txt, G.txt, @txt, and 7.txt. The [0-9].c string can be used for all the files in a directory that have a single digit before .c, such as 3.c and 8.c. The lab1/c string stands for lab1/c. Note the use of backslash (\ ) to quote (escape) the slash character (/).

The following command prints the names of all the files in your current directory that have two-character file names and an .html extension, with the first character being a digit and the second being an uppercase or lowercase letter. The printer on which these files are printed is spr.

```
$ lpr -P spr [0-9][a-zA-Z].html
$
```

Note that [0-9] means any digits from 0 through 9 and [a-zA-Z] means any lowercase or uppercase letter. The following command displays the names of all six-character-long files with .c extension in your current directory, with the first three characters being lab, the fourth being a digit, and the remaining being any two characters.

```
$ ls lab[0-9]?? .c
lab11a.c lab1a1.c lab123.c lab4ab.c
$
```

# 2.10 THE SUDO AND SU COMMANDS

The sudo command allows a permitted user to execute a command as the superuser, or to assume the role of another user, as specified by security policy. The su command allows an ordinary user to switch user roles or to also simulate being the superuser on the system. The superuser has file permission and access privileges to everything on the system.

In many of the operations shown in the following chapters, particularly in Chapter 23 on system administration, it will be necessary to execute the su command in order to accomplish the tasks shown. In order to use this command, it is necessary to know the root or superuser password.
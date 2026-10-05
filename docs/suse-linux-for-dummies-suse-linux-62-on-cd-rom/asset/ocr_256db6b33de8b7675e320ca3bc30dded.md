# 180 Part III: Using Linux

Note that the second line, we typed two accent grave characters, not apostrophes.

Single commands that are not separated by a pipe symbol — that is, their standard output won't be fed to the standard input of the next command — may be placed on the same line and separated with a semicolon (;). This shortcut is useful in interactive mode because you don't have to press Enter and wait for a response, but it saves any time in scripts. In scripts, it's better to put commands on separate lines so that they are easier to change if necessary.

![](bbox=[0.135, 0.183, 0.213, 0.268])

Suppose you run the program on the first day of the month over several months' time. You accumulate several copies of the passwd file, each with changes as login accounts are added and deleted.

Eventually, the reports directory looks somewhat like this:

```
maddog@localhost:~/reports > ls
passwd199807 passwd199809 passwd199711 passwd199901
passwd199808 passwd199810 passwd199812 passwd199902
maddog@localhost:~/reports >
```

To simulate your genreport program over several months, follow these steps:

+   1. Create a directory called reports, and change to that directory (type cd).

+   2. Execute the genreport program once.

+   3. Create seven copies of the report file for different months.

To do so, change the name of each new file to a different date. This creates eight files altogether (the original and seven copies). The files have the same contents, but that's for now.

```
passwd199807 passwd199808
passwd199807 passwd199809
passwd199807 passwd199810
passwd199807 passwd199811
passwd199807 passwd199812
passwd199807 passwd199901
passwd199807 passwd199902
```

+   4. Write a shell script that shows you the accounts that were added and deleted from month to month.

One way to do this is to create a program that allows you to supply the names of the two files to see whether any accounts have been added or deleted. The second way is more automated; have the program
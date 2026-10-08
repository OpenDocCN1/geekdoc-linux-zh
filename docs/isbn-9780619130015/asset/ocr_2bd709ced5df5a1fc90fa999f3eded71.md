![](bbox=[0.05, 0.07, 0.16, 0.125])

**tip**

> Remember your password! You need your password everytime you log on to UNIX.

# ## Viewing Files Using the cat, more, less, head, and tail Commands

Three UNIX commands let you view the contents of files: cat, more, and less. The more and less commands display a file, one screenful at a time, while the cat command displays the whole file at once. Two other commands, head and tail, let you view the first few or last few lines of a file.

The cat command gets its name from the word concatenate, which means to link. You can display multiple files by entering their file names after the cat command and separating each with a space. UNIX then displays the file’s contents in the order you entered them.

Your system administrator at Dominion mentions that you can use the cat command to view a file called shells that resides in the /etc directory. This file contains a list of valid shell programs on the system.

**To view the shells file:**

+   1.  Type `cat /etc/shells` after the command prompt, and press **Enter**.
Use the forward slash (//) to indicate a directory or folder change. You see a list of the available shells, including `/bin/bash`, `/bin/sh`, `/bin/bash`, `/bin/tcsh`, `/bin/csh`, and `/bin/zsh`.
Sometimes it is helpful to see a file’s contents displayed with line numbers. The `-n` option causes the `cat` command to display a number at the beginning of each line of output.
2.  Type `cat -n /etc/shells` and press **Enter**. You see the same list of shells as before, but this time a number precedes each line.

You can also view another file in the /etc directory called termcap. This multiple-page file contains many specifications about all terminals supported on the Linux system. The cat command is not a practical way to view this file, which is longer than one screen. However, you can use the more and less commands to read a large file screen by screen.

**To view the contents of large files on the screen with the more command:**

+   1.  Type `more /etc/termcap` after the command prompt, and press **Enter**.
2.  Press the **spacebar** to scroll to the next screen.
3.  Terminate the display by typing **q** (for quit).
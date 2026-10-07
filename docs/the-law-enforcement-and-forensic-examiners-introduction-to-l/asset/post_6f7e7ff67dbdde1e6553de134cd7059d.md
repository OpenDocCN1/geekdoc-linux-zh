
# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

- * Note that changes made to this file may be lost during upgrades. Another method is to create an executable file in the directory /etc/profile.d. Executable files placed in that directory are run at the end of /etc/profile.
- /home/$USER/.bash_profile This script is located in each user's home directory ($USER) and can be edited by the user, allowing him or her to customize their own environment. In this file you can add aliases to change the way commands respond. Note that the dot in front of the filename makes it a "hidden" file.
- /home/$USER/.bash_history - This is an incredibly useful file for a number of reasons. It sets a number of commands that have already been typed on the command line (default is 500). These are accessible through either "reverse shells" or by simply using the "up" arrow on the keyboard to scroll through the history of already-used commands. Instead of re-typing a command over and again, you can access it from the history.
- From the perspective of a forensic examiner, if you are examining a Linux system, you can access each user's (don't forget root) .bash_history file to see what commands were run from the command line. Remember that the leading "." in the file name signifies that it is a hidden file.

Keep in mind that the default values for /.bash_history (number of entries, history file name, etc.) can be controlled by the user(s). Read **man bash** for more detailed information.

The startup sequence is actually more complicated than this, but should give you a starting point. In addition to the above files, check out /home/$USER/.bashrc. The **man** page for bash is an interesting (and long) read, and will describe some of the customization options. In addition, reading the **man** page will give a good introduction to the programming power provided by bash scripting. When you read the **man** page, you will want to concentrate on the INVOCATION section for how the shell is used and basic programming syntax.

> In bash we define the contents of a variable with a dollar sign. $USER is a variable that represents the name of the current user. To see the contents of shell individual variables, use "echo $VARNAME".

## IV. Basic Linux Commands

A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

Linux at the terminal

Directory listing:

- ls : list files
- ls -F : classifies files and directories
- ls -a : show all files (including hidden)
- ls -l : detailed file list (long view)
- ls -lh : detailed list (long, with "human readable") file sizes

```
barry@forensic1:-$ ls -l
total 5195940
drwxr-xr-x 4 root root 4096 Aug 3 2013 Bootable/
drwxr-xr-x 2 root root 4096 Mar 5 15:45 Pictures/
drwxr-xr-x 2 root root 4096 Dec 11 13:44 Desktop/
drwxr-xr-x 2 root root 4096 Mar 24 15:31 LGPL/
-rw-r--r-- 1 root root 425741850 Aug 28 2016 swwre.tar.gz
```

We will discuss the meaning of each column in the ls -l output later in this document.

Changing Directories:

- cd dir : change directory to <>
- cd : (by itself) shortcut back to your home directory
- cd .. : up one directory (note the space between "cd" and "..")
- cd - : back to the last directory you were in.
- cd /dirname : change to the specified directory. Note that the addition of the "/" in front of the directory implies an explicit (absolute) path, not a relative one. This will make more sense.
- cd dirname : change to the specified directory. The lack of a "/" in front of the directory name implies a relative path meaning dirname is a subfolder of our current directory.

Copy files:

- cp source destination : copy source to destination
- cp -r source destination : copy directory recursively

Clear the Terminal: clears the terminal screen of all text and returns a **clear** prompt. <ctrl>-l (control-character-el) will accomplish the same.

Move a file or directory: move or rename a file.
**mv source destination**

- Delete a file or directory: deletes a file
**rm filename** recursively deletes all files in directories and all
**rm -r** remove directories (if empty)
**rmdir**
**rm -f** do not prompt for file removal

Display command help: display a "manual" page for the specified command.
**man command** use "q" to quit. VERY USEFUL

If you want to find information about a command called **find**, including its, options, etc., then you would use the "man page" for the command **find**:

```
barry@forensic1:~$ man find
FIND(1) General Commands Manual FIND(1)

NAME
find - search for files in a directory hierarchy

SYNOPSIS
find [-H] [-L] [-P] [-D debugopts] [-Olevel] [path...] [expression]

DESCRIPTION
This manual page documents the GNU version of find. GNU find searches the directory tree rooted at each given name
```

...

Create a directory: Creates a directory. Again, remember the **mkdir directory** difference between a relative and explicit path here.

Display the contents of a file:

- cat : The simplest form of file display, **cat** streams the contents of a file to the standard output (usually the terminal). **cat** actually stands for "concatenate".

- **cat file1 > file2** : Takes the contents of file1 and streams the output which is redirected to a single file, file3. This effectively adds the two files into one single file (the original files remains unchanged).

- **more filename** : displays the contents of a file one page at a time. Unlike its DOS counter, GNU **more** takes filenames as direct arguments.

- **less filename** : **less** is better **more** - Supports scrolling in both directions, and a number of other powerful features. **less** is actually the GNU version of **more**, and on many systems you will find that **more** is actually a link to **less**. Use **q** to exit a **less**. Note that you can choose several options. For example:

```
barry@forensic1:-$ file pic.png
pic.png: PNG image data, 48 x 48, 4-bit colormap, non-interlace own```

ls -aF will give you a list of all files (-a), including hidden files, and classification (-F), which shows directories, "*" for executables, and "@" for links.

## Additional useful commands

**grep** searches for patterns.

**grep pattern filename**

**grep** will look for occurrences of pattern within the file. **grep** is an extremely powerful tool. It has hundreds of uses given the large number of options it supports.

find allows you to search for a file based on any number of criteria, dates dates sizes, name patterns, etc. To look for your fstab file, you might try:

```
barry@forensic1:-$ find -iname fstab
/etc/fstab
```

find, starting in the root directory (/), by name, fstab and print the results to the screen. The power of the find command should not be underestimated. More on this tool later. Have a look at man find. Can you see the difference between -iname and -name?

pwd presents the working directory to the screen. The following example shows that we are currently in the directory /home/barry.

```
barry@forensic1:-$ pwd
/home/barry
```

file categorizes files based on what they contain using a signature, regardless of the name (or extension, if one). Compares the file header to the "magic" file in an attempt to ID the file type. For example:

```
barry@forensic1:-$ file pic.png
pic.png: PNG image data, 48 x 48, 4-bit colormap, non-interlace
```

- ps list of current processes. Gives the process ID number (PID), and the terminal on which the process is running.

ps ax shows all processes (a), and all processes without an associated terminal (x). Note the lack of a dash in front of the options. See the man page for info on this departure from our previous convention.

```
barry@forensic1:-$ ps ax
STAT TIME COMMAND
1 ? Ss 0:00 init [4]
2 ? S 0:00 [kthreadadd]
3 ? S 0:00 [ksoftirqd/0]
5 ? S< 0:00 [kworker/0:0H]

1597 ? 0:00 [kworker/0:0]
1604 pts/1 Ss+ 0:00 -bash
1645 ? S 0:00 [kworker/1:0]
```

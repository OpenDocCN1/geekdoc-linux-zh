The export command makes a newly created environment variable available to other programs run from that environment. For example, to define a new environment variable called db_data that your database program requires, and then make that variable available to other programs besides the shell itself (including the database program), use these two commands:

```
$ DB_DIR=/usr/local/db_data
$ export DB_DIR
```

The shell itself relies on many environment variables. The online manual page for the bash shell lists dozens of variables that the shell uses (or can use, if you set them) to control or select features of the shell. Two of these variables are described here as examples.

The PATH environment variable contains a list of directories on the Linux system that the shell searches each time a command is executed. When you enter a program name to be run at the shell prompt, the shell searches in each directory listed in the value of the PATH variable. If the program is not found in the first directory, the second is searched, and so forth. The command to view the value of PATH is echo $PATH. Sample output of this command on Red Hat Linux is shown here. (The value of PATH varies depending on whether you are logged in as root or as a regular user. The output here is for a regular user account.)

```
$ echo $PATH
/usr/kerberos/bin:/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:/home/nwells/bin
```

Suppose you want to execute a program, but the directory in which the program is located is not part of the PATH variable. You must provide the shell with the file's complete pathname. For example:

```
$ /tmp/downloads/screensaver-sample
```

If you simply enter screensaver-sample alone, the shell looks in the PATH directories and is unable to find the program. An interesting exercise is to press the Tab key twice on an empty shell prompt line. The shell attempts to use tab completion, but because you have entered no characters, the list of possible matches is very large—it includes all of the executable programs from every directory listed in the PATH variable. When you do this (press Tab twice), the shell requests confirmation with a message such as this one:

```
Display all 3636 possibilities? (y or n)
```

Pressing the "y" key for "yes" causes the shell to list all of the executable programs that it can find in the PATH directories.

Another environment variable used by the shell is PS1. This variable defines the shell prompt for bash. Note the default value:

```
$ echo $PS1
```

```
[\u@\h \W]\$
```
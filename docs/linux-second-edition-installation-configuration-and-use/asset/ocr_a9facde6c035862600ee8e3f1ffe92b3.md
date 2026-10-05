of the shell program with a dot and a space (this is the short notation for the shell
command source).

An example: you want to write a shell program which adds the path to the
current directory to the environment variable PATH. The necessary program addpwd is
very simple:

```
# /bin/sh
# shell program addpwd adds the current directory to the path
#
PATH=$PATH:$(pwd)
```

Thus, the variable PATH is assigned its previous contents, a colon; and finally,
via command substitution, the result of the pwd command. The following test run
shows the contents of the PATH variable in the current shell are only changed
when addpwd is started with a preceding dot. (Inside the shell that was started at
the first call of addpwd, PATH is obviously changed – this change, however, is valid
only as long as addpwd is running).

```
user$ echo PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:sbin:
/usr/bin/X11:/usr/bin/bin:/usr/openbin/bin:/usr/games:
user addpwd
user$ echo PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:sbin:
/usr/bin/X11:/usr/bin/bin:/usr/openbin/bin:/usr/games::/home/mk/book
```

# Variables predefined by the shell

Inside shell programs, several variables predefined by the bash can be accessed.
These variables cannot be changed through assignments; they can only be read. The
names of the variables are constructed from various special characters. In the following-table, the variables are indicated with their preceding $ symbol.

+   $ variables
$? return value of the last command
$! PID of the most recently started background process
$$ PID of the current shell
$0 file name of the currently executed shell script (or of the
symbolic link that points to the file)
## number of parameters passed to the shell program
$1 to $9 parameters 1 to 9
$* or $@ total of all parameters passed

Some additional remarks about the application of these variables: $0 to $9, ##
 and $* are used for the evaluation of the parameters passed to the batch program.
Nearly every sample script in this chapter shows their use.
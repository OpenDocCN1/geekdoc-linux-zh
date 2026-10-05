# COMMAND REFERENCE

-r or -R --recursive
also deletes files in all subdirectories (warning!). When the entire contents of a
ubdirectory are deleted, the subdirectory itself is deleted as well.

# Examples

```
user$ rm *
deletes backup files (files whose names end with "*") in the current directory.
user$ rm -backup
```

deletes the file or the directory backup. When backup is a directory, all subdirectories
and files in it are deleted too!
user$ rm '#*'

deletes all files whose begin with the symbol #. The quotes are necessary to
prevent the shell from interpreting the # character as a comment.

# rmdir [options] directory

rmdir deletes the specified directory, rmdir can only be executed when the directory
is empty. Any existing files must previously be deleted with rm (if necessary, using
t -r option). The most important option is:
-p or --parents
alletes subdirectories in the specified directory (provided that the directo-
ries not contain any files).

# sed [options] command [< source >

sed is a so-called stream editor. The command is normally used as a text filter to find
and process (delete, substitute with other characters, and so on) given characters or
character combinations in the source text. sed is controlled by commands which are
aplied to all lines of the text or only to lines that satisfy given conditions.
Unfortunately, handling sed is rather complicated, and because of the many
characters. For these reasons, we will do without a detailed
description and give two examples:
user$ sed 1,3d test

deletes the first three lines of the file test and displays the rest of the file on
screen (standard output). Here, d stands for the sed command delete. 1,3 specifies
address range sed to which this command is applied.
user$ sed s/a/A/ < test

replaces 'a' with 'A'. Here, s stands for the command regular find and replace.
the texts enclosed in / are the search pattern and the replacement text. Since no
address range is specified, the command is applied to all lines.
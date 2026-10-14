# The Linux Cookbook: Tips and Techniques for Everyday Use:

-iregex regexp Path name of file, relative to specified directory tree, matches the regular expression regexp, regardless of case (`t?p' matches `TIP' and `top').

-links links Number of links to the file (see section Giving a File More than One Name).

-mmin minutes Number of minutes since the file's data was last changed.

-mtime days Number of days since the file's data was last changed.

-name pattern Base name of the file matches the pattern pattern.

-newer file File was modified more recently than file.

-path pattern Full path name of file matches the pattern pattern(`./r*r t' matches `./records/report').

-perm access mode File's permissions are exactly access mode (see section Controlling Access to Files).

-regex regexp Path name of file, relative to specified directory tree, matches the regular expression regexp.

-size size File uses size space, in 512-byte blocks. Append size with `b' for bytes or `k' for kilobytes.

-type type File is type type, where type can be `d' for directory, `f' for regular file, or `l' for symbolic link.

-user user File is owned by user.

The following table lists and describes find's options for specifying what to do with the files it finds.

OPTION DESCRIPTION
-exec commands Specifies commands, separated by semicolons, to be executed on matching files. To specify the current file name as an argument to a command, use `{}'.
-ok commands Like `-exec' but prompts for confirmation before executing commands.
-print Outputs the name of found files to the standard output, each followed by a newline character so that each is displayed on a line of its own. On by default.
-printf format Use "C-style" output (the same as used by the printf function in the C programming language), as specified by string format.

The following table describes the variables may be used in the format string used by the `-printf' option.

VARIABLE DESCRIPTION
\a Ring the system bell (called the "alarm" on older systems).
\b Output a backspace character.
\f Output a form feed character.
\n Output a newline character.
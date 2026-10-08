-p Put a slash (/) at the end of directory names.

-q Nonprinting characters are represented by a "?".

-r Reverse the order in which files are printed.

-s Show the size in blocks instead of bytes.

-t List in order of time saved, with most recent first.

-u Use the time of last access instead of last modification for determining order in which files are printed.

-x List files in multicolumn format as shown in examples.

-A Same as -a, except that current and parent directories aren't listed.

-C Multicolumn output produced.

-F Directory followed by a "/", executable by an "*", symbolic link by an "@", and FIFO by a "|".

-L List file or directory to which link points.

-R Recursively list subdirectories.

-l Output will be listed in single-column format.

Also, some shorthand command names are available for issuing ls with options. For instance, ll is equivalent to ls -l, and lsr is equivalent to ls -R in some UNIX variants. We will also cover creating an "alias," whereby you can define your own shorthand for any command in an upcoming chapter.

You can selectively list and perform other file-related commands with wild cards. The following section covers file name expansion and wild cards.

# File Name Expansion and Wild Cards

Before we cover additional file system related commands, it is worth taking a look at file name expansion. An overview of file name expansion is useful to ensure that you're comfortable with this topic before we cover additional commands.
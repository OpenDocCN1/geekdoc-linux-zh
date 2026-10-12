# PART III

Over time, especially in Linux, people have customized the man pages to include other optional fields. Some of these fields are Author, Sort Keys, Updating, and Notes. The additions have been made to enhance the pages. For example, the Author section many times includes an author's email address, which is handy if the command is not working as you expected it to. (Remember, none of Linux was taken from UNIX, so small differences do exist, even in the "standard" commands.)

Probably the one thing to point out to new man page users is the syntax used for showing the command's synopsis. Several standards are followed in writing commands that are used in the man pages. Here's the synopsis for the `ps` command:

```
SYNOPSIS
ps [ - ] [ 1u ] [ smaxSecwrnu ] [ txt ] [ 0 [ + ] . K [ + ] . K 2 . . . ] [ pids ]
```

Anything in square brackets ([]) is optional. Note that the only thing not optional in this command is the command itself. Therefore, you can issue the `ps` command without any options and you will receive a snapshot of the current processes.

[ - ] means that the - is an optional argument. Many commercial versions of UNIX require a dash to indicate that what follows are arguments. This is not true for the Red Hat Linux version of the `ps` command. The next set of characters (between the next set of square brackets) indicates that any of these parameters can be added to the `ps` command. For example, `-1a` is a common set of parameters to add to the `1s` command; it displays a long list of all files, including hidden files.

The man pages are not a singular file or directory of Linux manuals. Instead, the man pages are a set of directories, each containing a section of the man pages. These directories contain the raw data for the man pages. Red Hat Linux has eight sections of man pages. In addition, each section has corresponding catn subdirectories that store processed versions of the man pages. When a man page is accessed, the program that formats the man pages saves a copy of the formatted man page in the catn (\texttt{/var/catman/catn}) directories. (This location can be changed in the \texttt{/etc/man.config} file to point to another location.) This saves time in the future; the next time a user requests a man page for a subject that has been accessed before, the formatting does not have to be repeated. Instead, it can be displayed from the previously formatted page. The following shows what information appears within each section:

| Section | Content |
|---|---|
| 1 | User commands |
| 2 | System calls |
| 3 | Functions and library routines |
| 4 | Special files, device drivers, and hardware |
Remove all the files in a directory:

```
rm -i mydirectory/*
```

Note that the previous command removes files only, and does not remove any directories in mydirectory.

Remove a file in the current directory whose name starts with `-` or `*` or some other character that is special to the shell:

```
rm .~-filename
rm \*filename
etc.
```

Remove a file in the current directory whose name starts with some strange (usually nonprinting, invisible) character or perhaps has spaces at the beginning or end of the filename, prompting for confirmation:

```
rm -i *filename*
```

If *filename* is not unique in the directory, enter n when each of the other files is prompted.

A powerful and dangerous command to remove a directory is:

```
rm -fR directoryname
```

or

```
rm -Rf directoryname
```

which removes all files and directories from directoryname without any prompting for verification to remove the files or the directories. This command should only be used when you are absolutely certain that all the files and directories in directoryname as well as directoryname itself are to be removed.

# DEPENDENCIES

NFS

rm does not display a plus sign (+) to indicate the existence of optional access control list entries when asking for confirmation before removing a networked file.

# SEE ALSO

rmdir(1), unlink(2), acl(5).

# STANDARDS CONFORMANCE

rm: SVID2, SVID3, XPG2, XPG3, XPG4, POSIX.2
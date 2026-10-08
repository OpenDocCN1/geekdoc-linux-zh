# Make Hard or Symbolic Links to Files

Synopsis

```
/usr/bin/ln [-fns] source-file [target]
/usr/bin/ln [-fns] source-file...
/usr/xpg4/bin/ln [-fs] source-file [target]
/usr/xpg4/bin/ln [-fs] source-file...
```

Description
At times it is useful to have one accessible file from several directories. Reduce the amount of disk space used and make it easier to maintain consistency in files used by several people. Use the ln (link) command to create links between directory entries in a single file system to make a single file at two or more locations in the directory hierarchy.

Symbolic links (-s) can link files across file systems. A symbolic link has a name and a location in the directory tree but has no contents. It points to any other file or directory.

Use the ln command to create both hard and symbolic links. A hard link is a pointer to a file and is indistinguishable from the original directory entry. Any changes to a file are effective independently of the name used to refer the file. Hard links cannot span file systems and cannot refer to directories.

By default, ln creates hard links. source-file is linked to target. If target is a directory, another named source-file is created and linked to the original source-file.

In the first synopsis form, the ln creates a new directory entry (link) for the file specified by source-file, at the destination path specified by target. If you do not specify target, the link is made in the current directory. This first synopsis is assumed when the final operand does not name an existing directory; if you specify two operands and the final operand is not an existing directory, an error occurs.

In the second synopsis form, the ln creates a new directory entry for each file specified by source-file at a destination path in the existing directory named target.

```
/usr/bin/ln
```

If target is a file, its contents are overwritten. If /usr/bin/ln determines that the mode of target forbids writing, it prints the message (see chmod(1)), asks for a response, and reads the standard input for input. If the response is affirmative, the link occurs permissible; otherwise, the command exits

```
/usr/xpg4/bin/ln
```

If target a file and you do not specify the -f option, /usr/xpg4/bin/ln writes a diagnostic message to standard error, does nothing with the current source-file, and goes on to any remaining source-files. A symbolic link is an indirect pointer to a file; its directory entry contains the name of the file to which it is linked. Symbolic links can span file systems and can refer to directories.

When you create a hard and the source file is itself, a symbolic link, the target is a hard link to the file referred by the symbolic link, not to the symbolic object itself(source_file).

File permissions for target can differ from those displayed with a -l listing of the ls(1) command. To display the permissions of target, use ls -lL. See stat(2) for more information.

![](bbox=[0.068, 0.863, 0.108, 0.893])
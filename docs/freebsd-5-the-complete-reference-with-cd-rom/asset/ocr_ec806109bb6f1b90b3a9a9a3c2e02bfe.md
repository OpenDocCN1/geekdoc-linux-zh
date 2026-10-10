> Mass file copying can also be accomplished with tar, which is described in the upcoming section, "Backing Up." In fact, tar is more reliable at duplicating certain file characteristics, and so is preferred if you need the best possible copy of a directory, as when you're moving files to a new hard disk.

# Using mv

The mv command is similar in syntax and operation to cp, but it lacks a recursive function. This command moves, rather than copies, files. In practice, it's also used to rename files—"moving" a file from a directory to the same directory but under another name serves as FreeBSD's renaming command. The syntax for this command can be described as follows:

```
mv [-f | -i] [-v] source target
mv [-f | -i] [-v] source[...] target-dir
```

The options to this command are the same as those for cp. In practice, mv sometimes works much as does cp, by copying files, but it then deletes the originals. This happens when the target directory is on another filesystem, such as a mounted floppy or Zip disk. When moving files within a single filesystem, though, FreeBSD can create a new directory entry in the target location and then delete the original directory entry, without moving the file's contents. This process can make moves within a filesystem very fast, even when the files are very large.

# Using cat

The cat command name is short for concatenate, and it's a tool that's used to combine multiple files into one. In practice, it's also often used to view the contents of a single text file. The command's syntax is

```
cat [-bvnetsu] [file [...]]
```

Ordinarily, cat writes to standard output (stdout), so to use it for file copying, you must use redirection, as described in Chapter 5. The options to cat are

+   - **b** This option adds line numbers to the output. (Blank lines are not numbered.)
+   - **n** This option adds line numbers to the output. (Blank lines are numbered.)
+   - **v** This option displays nonprinting characters using printable codes, such as ^X for CTRL-X.
+   - **t** This option is the same as -v, but TAB characters are displayed as ^ I.
+   - **e** This option is the same as -v, but the ends of lines are marked with dollar signs ($).
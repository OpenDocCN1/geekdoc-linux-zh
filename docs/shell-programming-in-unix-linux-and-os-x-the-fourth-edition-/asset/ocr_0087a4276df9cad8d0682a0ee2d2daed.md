To copy a file from another directory into your current location in the file system and give the file the same name, use the handy “.” shortcut for the current directory:

```
```text
$ pwd
/users/steve/misc
$ cp ../programs/collect .
$
```
```

The preceding command copies the file `collect` from the directory `../programs` into the current directory (`/users/steve/misc`).

# Moving Files Between Directories

You recall that the `mv` command can be used to rename a file. Indeed, there is no “rename” command in Unix. However, when the two arguments reference different directories, the file is actually moved from the first directory into the second.

To demonstrate, go from the home directory to the `documents` directory:

```
```text
$ cd documents
$
```
```

Suppose that now you decide that the file `plan` contained in the `memos` directory is really a proposal so you want to move it from the `memos` directory into the `proposals` directory. The following would do the trick:

```
```text
$ mv memos/plan proposals/plan
$
```
```

As with the `cp` command, if the source file and destination file have the same name, only the name of the destination directory need be supplied, so there’s an easier way to move this file:

```
```text
$ mv memos/plan proposals
$
```
```

Also like the `cp` command, a group of files can be simultaneously moved into a directory by simply listing all files to be moved before the name of the destination directory:

```
```text
$ pwd
/users/steve/programs
$ mv wb collect mon ../misc
$
```
```

This would move the three files `wb`, `collect`, and `mon` into the directory `misc`.

You can also use the `mv` command to change the name of a directory, as it happens. For example, the following renames the `programs` directory to `bin`.

```
```text
$ mv programs bin
$
```
```
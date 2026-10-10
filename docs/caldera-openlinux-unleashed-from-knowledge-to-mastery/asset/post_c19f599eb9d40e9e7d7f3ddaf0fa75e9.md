
## Warning

`cp` also has a `-r` option that does almost the same thing as `-R`; do not use it. The `-R` option copies special files, such as device files, correctly; the `-r` option assumes that all non-directory files are normal files and tries to read them as normal files. This could cause serious problems if the hierarchy you are copying contains device files.

- `-p` Preserves the original files' owner, group, permissions, and modification and access times. (The owner and group can only be preserved if you run `cp` as root.)
- `-d` Does not follow symbolic links. Normally, `cp` treats symbolic links as normal files and copies the files to which they point. The `-d` option causes it to copy only the link itself. This option is not standardized by POSIX; it is available only with GNU `cp`.
- `-a` Preserves as much of the original structure and attributes of the original tree as possible. The `-a` option is equivalent to `-dpR`.

`cp` has many more options for such things as making symbolic links instead of actual copies and making versioned backups of destination files. Consult `cp (1)` for details.

### Finding Files: `find`

The `find` command is one of the most powerful and useful commands in UNIX. It’s also fairly hard to master.

Essentially, `find` does the following:

- Starts from an initial path (or set of paths)
- Finds files that meet certain criteria
- Does something with the filenames

Thus, you supply three pieces of information to `find`:

- The starting path
- The criteria for files you’re interested in
- The action to be taken when an interesting file is found

Let’s look at an example before diving into the syntax:

```
$ find /usr/doc -name '*mail*' -print
/usr/doc/fetchmail-4.7.7
/usr/doc/fetchmail-4.7.7/fetchmail-FAQ.html
...
```

The three pieces of information for the example are:

- The initial path: `/usr/doc`.
- The criteria: `-name '*mail*'`. In this case, this is a single criterion saying “Match all files or directories whose names contain mail.” (The `*mail*` part is quoted to prevent the shell from expanding it.)
- The action: `-print`. This tells `find` to print the names of matching files.

The following is another example:

```
$ find /usr/doc -type f -name '*mail*' -print
/usr/doc/fetchmail-4.7.7/fetchmail-FAQ.html
/usr/doc/fetchmail-4.7.7/fetchmail.lsm
...
```

This example added an additional criterion: `-type f`. This tells `find` to accept only plain files, not directories (or device files). If there are several criteria on the command line, as in the example, all must be met for the action to be triggered. Thus, the example prints the names of all ordinary files under `/usr/doc` whose names contain “mail”.

### `find` Syntax

The overall syntax of `find` is:

```
find [paths…] [expression]
```

If the `paths` are omitted, the path list defaults to the current directory. If `expression` is omitted, it defaults to `-print`.

![](img/df365d352a104b50fea29e59a052de4d_968_0.png)

Thus, a bare `find` will print the entire directory hierarchy rooted at the current directory.

The `expression` contains four types of terms that return `true` or `false`:

- **Options**—Affect the overall operation rather than the processing of a particular file. Options always return `true`.
- **Tests**—Return `true` or `false`.
- **Actions**—Have side effects and can return `true` or `false`.
- **Operators**—Alter the results of a test or combine two tests together.

Normally, the expression is evaluated from left to right for each file. As soon as any term returns false, `find` moves to the next file. Otherwise, if the end of the expression is reached and no action has been taken, `find` invokes the `-print` action.

### Options

Options always take effect rather than being processed only as `find` moves through the expression. For clarity, you should place options at the beginning of the expression. Table A.3 lists and describes some important options.

**TABLE A.3 Options**

| Option | Description |
| :--- | :--- |
| -depth | Process the contents of a directory before the directory itself. This causes find to move through a hierarchy in a depth-first manner. |
| -follow | Follow symbolic links. Normally, they are not followed. |
| -maxdepth levels | Descend at most levels (a non-negative integer) levels of directories below the paths supplied on the command line. |
| -mindepth levels | Descend at least levels (a non-negative integer) levels of directories below the paths supplied on the command line before applying any tests or performing any actions. |
| -mount or -xdev | Do not descend into directories on other file systems. |

For example, to find and list all files larger than 100KB but only in the current directory (not in any subdirectories), use:

```
$ find . -maxdepth 1 -size +100k -ls
```

### Tests

Many tests take a numeric argument. This argument can be specified in one of three ways:

- `+n` Greater than n.
- `-n` Less than n.
- `n` Exactly n.

The following are some useful tests:

- `-atime n` true if the file was last accessed n days ago. For example, to find all files that haven't been accessed in seven days or more, use:

```
$ find path -atime +6 -print
```

To find files that have been accessed in the last day, use:

```
$ find path -atime -2 -print
```

- `-ctime n` true if the file's status was changed n days ago.
- `-empty` true if the file is a plain file or directory and is empty.
- `-fstype type` true if the file system containing the file is of type type. Common values for type are ext2 for normal Linux file systems, proc for the /proc pseudo-file system, and iso9660 for CD-ROM file systems.
- `-gid n` true if the file's numeric group ID is n.
- `-group gname` true if the file's group is gname.
- `-name pattern` true if the file's base name (with leading directories removed) matches the shell pattern pattern.
- `-iname pattern` Like -name, but matching is case-insensitive.
- `-mtime n` true if the file's contents were last modified n days ago.
- `-newer otherFile` true if the file was modified more recently than otherFile.
- `-perm mode` true if the file's permission bits are exactly mode.
- `-perm -mode` true if all the bits in mode are set for the file.
- `-perm +mode` true if any of the bits set in mode are set for the file.
- `-size n[bcwk]` true if the file uses n units of space. A “unit” is 512 bytes, unless a letter follows n. In this case, c makes a unit one byte, k makes a unit one kilobyte, b makes a unit 512 bytes, and w makes a unit two bytes.
    - For example, to find all files under your home directory that are larger than one megabyte, use:

```
$ find $HOME -size +1024k -print
```

- `-type x` true if the file is of type x, where x is one of the following:
    - b A block device
    - c A character device
    - d A directory
    - f A regular file
    - l A symbolic link
    - p A named pipe (FIFO)
    - s A socket

![](img/df365d352a104b50fea29e59a052de4d_970_0.png)

## Note

I have not yet discussed named pipes or sockets yet. They are two special kinds of files used for inter-process communication (IPC).

- `-uid n` true if the file’s numeric user ID is n.
- `-user uname` true if the file is owned by user uname.

### Actions

An action term in an expression can appear anywhere a test does. It can return true or false, but has side effects. The following are some useful actions:

- `-exec command` Executes command. Returns true if the command executes without errors. All the arguments following -exec are taken as part of the command until an argument consisting of a semicolon is found. The string `{}` is replaced by the filename being processed.

## Warning

You must escape the semicolon so it is not interpreted by the shell.

For example, let’s say you have a text editor that makes backup files named filename.bak and you want to delete all such files from your home directory. Use:

```
$ find $HOME -name "*.bak" -print -exec rm {} \;
```

Let’s dissect this command:

1. The command starts looking for files in your home directory ($HOME).
2. It looks for files named "*.bak". Note how the shell pattern was quoted to prevent the shell from expanding it.
3. As it finds each matching file, it prints the name.
4. It also removes the file by executing the command rm filename. Note how the curly braces {} are replaced by the filename. Note also how the terminating semicolon was escaped with a backslash.

- `-ok command` Similar to -exec, but prompts for confirmation before executing the command.
- `-print` Prints the name of the file on standard output followed by a newline. Always returns true.

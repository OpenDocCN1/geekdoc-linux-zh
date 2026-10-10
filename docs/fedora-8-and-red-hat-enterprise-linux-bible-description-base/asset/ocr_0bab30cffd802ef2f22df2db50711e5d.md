> **CAUTION**: The `­R` option of `chmod` works best if you are opening permissions completely or adding execute permission (as well as the appropriate read/write permission). The reason is that if you turn off execute permission recursively, you close off your ability to change to any directory in that structure. For example, `chmod -R 644 /tmp/test` turns off execute permission for the `/tmp/test` directory, and then fails to change any files or directories below that point.

# Moving, copying, and deleting files

Commands for moving, copying, and deleting files are fairly straightforward. To change the location of a file, use the `mv` command. To copy a file from one location to another, use the `cp` command. To remove a file, use the `rm` command. Here are some examples:

```
$ mv abc def
$ mv abc -
$ cp abc def
$ cp abc -
$ rm abc
$ rm *
```

Of the two move (`mv`) commands, the first moves the file `abc` to the file `def` in the same directory (essentially renaming it), whereas the second moves the file `abc` to your home directory (`-`). The first copy command (`cp`) copies `abc` to the file `def`, whereas the second copies `abc` to your home directory (`-`). The first remove command (`rm`) deletes the `abc` file; the second removes all the files in the current directory (except those that start with a dot).

> **CAUTION**: Be sure to use the * and other wildcard characters wisely, because you might match (and therefore remove) files you don't intend to match.

> **NOTE**: For the root user, the `mv`, `cp`, and `rm` commands are aliased to each be run with the `­i` option. This causes a prompt to appear asking you to confirm each move, copy, and removal, one file at a time. This is done to prevent the root user from messing up a large group of files by mistake. To temporarily get around an alias, type the full path to the command (for example, `/bin/rm -rf /tmp/junk/*`).

# Using the vi Text Editor

It's almost impossible to use Linux for any period of time and not need to use a text editor. If you are using a GUI, you can run `gedit`, which is fairly intuitive for editing text. Most Linux shell users will use either the `vi` or `emacs` commands to edit text files. The advantage of `vi` or `emacs` over a graphical editor is that you can use it from any shell, a character terminal, or a character-based connection over a network (using `telnet` or `ssh`, for example). No GUI is required.
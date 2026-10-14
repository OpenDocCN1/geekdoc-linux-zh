⇒ To output a verbose listing of the /usr/share/doc/bash directory, giving all numbers in a human readable form, type:

```
$ ls -lh /usr/share/doc/bash [RET]
```

This command outputs a verbose listing of the files in the /usr/share/doc/bash directory, giving all numbers in a human readable form, as in Figure 5-5.

# 5.3.4 Listing Hidden Files

By default, ls does not output files that begin with a period character (.). To reduce clutter, many applications “hide” configuration files in your home directory by giving them names that begin with a period; these are called dot files, or sometimes “hidden” files. As mentioned earlier, every directory has two special dot files: .., the parent directory, and ., the directory itself.

To list all contents of a directory, including these dot files, use the -a option.

⇒ To list all files in the current directory, type:

```
$ ls -a [RET]
```

Use the -A option to list almost all files in the directory: it lists all files, including dot files—with the exception of the .. and . directory files.

⇒ To list all files in the current directory except for . and .., type:

```
$ ls -A [RET]
```

# 5.3.5 Listing Directories in Columns

Use the -1 option to list a directory in a single column. Files will be listed one to a line. This is good for cut and pasting.

⇒ To list the contents of /usr/bin in a single column, type:

```
$ ls -1 /usr/bin [RET]
```

When output from ls is piped to anywhere but the terminal, ls uses this single-column format.

Normally, ls lists files in columns going vertically—first the leftmost column will be filled, and then the next column, all the way over toward the right side of the screen. Use -x to make the columns list horizontally instead—so that the first line across is filled with file names first, and then the next line, until all files are listed.
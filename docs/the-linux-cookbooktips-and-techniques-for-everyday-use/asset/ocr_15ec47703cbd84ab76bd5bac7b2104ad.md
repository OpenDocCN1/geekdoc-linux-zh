# 8.3.2 Finding the Smallest Files in a Directory

To list the contents of a directory with the smallest files first, use `ls` with both the `-S` and `-r` options, which reverses the sorting order of the listing.

+   - To list the files in the current directory and their attributes, sorted from smallest to largest, type:

```
```sh
$ ls -lSr RET
```
```

# 8.3.3 Finding the Smallest Directories

To output a list of *directories* sorted by their size—the size of all the files they contain—use `du` and `sort`. The `du` tool outputs directories in ascending order with the smallest first; the `-S` option puts the size in kilobytes of each directory in the first column of output. Give the directory tree you want to output as an option, and pipe the output to `sort` with the `-n` option, which sorts its input numerically.

+   - To output a list of the subdirectories of the current directory tree, sorted in ascending order by size, type:

```
```sh
$ du -S . | sort -n RET
```
```

# 8.3.4 Finding the Largest Directories

Use the `-r` option with `sort` to *reverse* the listing and output the largest directories first.

+   - To output a list of the subdirectories in the current directory tree, sorted in descending order by size, type:
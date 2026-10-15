# EXPLANATION

+   1 Lists all available shells on this Linux system.
+   2 Asks the user to type in the full pathname for a new login shell. Fails unless a full pathname, such as /bin/tcsh, is given.

# clear—clears the terminal screen

# cmp—compares two files

```
cmp [ -l ] [ -s ] filename1 filename2
```

The two files are compared. cmp makes no comment if the files are the same; if they differ, it announces the byte and line numbers at which the first difference occurred.

# EXAMPLE A.13

```
cmp file.new file.old
```

# EXPLANATION

If the files differ, the character number and the line number are displayed.

# compress—compress, uncompress, zcat compress, uncompress files, or display expanded files

```
compress [ -cfv ] [ -b bits ] [ filename... ]
uncompress [ -cv ] [ filename... ]
zcat [ filename... ]
```

compress reduces the size of the named files using adaptive Lempel-Ziv coding. Whenever possible, each file is replaced by one with a .Z extension. The ownership modes, access time, and modification time will stay the same. If no files are specified, the standard input is compressed to the standard output.

# EXAMPLE A.14

+   1 compress -v book
+   book:Compression:35.07% -- replaced with book.Z
+   2 ls
+   book.Z

# EXPLANATION
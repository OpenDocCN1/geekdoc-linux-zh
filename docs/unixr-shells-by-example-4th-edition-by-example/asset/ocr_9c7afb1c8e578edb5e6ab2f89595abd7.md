# 10.6.19 The filetest Built-In (tcsh)

The tcsh built-in filetest command applies one of the file inquiry operators to a file or list of files and returns a space-separated list of numbers; 1 for true and 0 for false.

# EXAMPLE 10.30

```
1 > filetest -rwf dirstack file.sc xxx
1 1 0
2 > filetest -b hdd
1
3 > filetest -lrx /dev/fd
1
```

# EXPLANATION

+   1 Each of the files, dirstack, file.sc, and xxx, are tested to see if they are readable, writable, plain files. For the first two files the test returns true (1 1), and for the last the test returns false (0).
+   2 The filetest command returns 1 if the file, hdd, is a block special device file. It is. Otherwise, 0 is returned.
+   3 The filetest command returns 1 if the file, fd, is a symbolic link and is readable and executable. It is. Otherwise, 0 is returned.

# 10.6.20 Additional TC Shell File-Testing Operators

There is an additional set of file-testing operators (tcsh only), shown in Table 10.10, that return information about files. Because the returned values are not true/false values, a -1 indicates failure (except F, which returns a ).

# Table 10.10 Additional tcsh File Tests

| Operator | What It Does |
|---|---|
| -A | Last file access time, as the number of seconds since the epoch (Jan. 1, 1970) |
| -A: | Like A, but in timestamp format, e.g., Fri. Aug. 27 16:36:10 2004 |
| -M | Last file modification time |
| -M: | Like M, but in timestamp format |
| -C | Last inode modification time |
| -C: | Like C, but in timestamp format |
| -F | Composite file identifier, in the form device:inode |
| -G | Numeric group ID |
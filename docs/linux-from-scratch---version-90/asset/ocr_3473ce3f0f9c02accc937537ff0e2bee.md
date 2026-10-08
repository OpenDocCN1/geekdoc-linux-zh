# 6.56. Diffutils-3.7

The Diffutils package contains programs that show the differences between files or directories.

Approximate build time: 0.4 SBU
Required disk space: 36 MB

# 6.56.1. Installation of Diffutils

Prepare Diffutils for compilation:

```
./configure --prefix=/usr
```

Compile the package:

```
make
```

To test the results, issue:

```
make check
```

Install the package:

```
make install
```

# 6.56.2. Contents of Diffutils

Installed programs: cmp, diff, diff3, and sdiff

# Short Descriptions

+   - cmp Compares two files and whether or in bytes they differ
- diff Compares two files or directories and reports which lines in the files differ
- diff3 Compares three files line by line
- sdiff Merges two files and interactively outputs the results
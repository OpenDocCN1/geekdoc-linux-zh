# # Viewing files and directories

The ls program probably is the most widely used program on any Unix or Unix-like platform. The most widely used options for ls are -l (long listing), -a (all files including filenames starting with a period), -1 (single-column, filenames-only listing), and -R (recursive listing).

# # Navigating your way into directories

You likely already know the cd command, which is really a built-in shell command. If you don’t provide a directory name as an argument, the cd command returns you to the home directory of the user account you are currently using. Any time you are in doubt about where you are in the file system, use the pwd command, which displays your current directory name.

# # Determining file type

Unlike Microsoft Windows operating systems, Linux does not rely on file extensions to determine file types. Use the file utility to determine a file’s type. For example,

```
```
file /usr/bin/file
```
```

shows what type of file /usr/bin/file (itself) is. Here is an example of its output:

```
```
/usr/bin/file: ELF 32-bit LSB executable, Intel 80386, \
version 1, dynamically linked, not stripped
```
```

# # Viewing the access statistics of a file or directory

You can use the stat program to get statistics on a file or directory. For example,

```
```
stat /tmp
```
```

shows statistics on the /tmp directory. Here is an example of its output:

```
```
File: "/tmp"
```
```
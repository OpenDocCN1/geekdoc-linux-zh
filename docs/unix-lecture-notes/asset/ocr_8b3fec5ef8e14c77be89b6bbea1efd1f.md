textual input. They are specifically designed for that purpose. Although you could read structures by reading one char at a time and then reconstructing the structure from the sequence of chars with a lot of type casts, that would be grossly inefficient and error-prone. Clearly there must be a better way.

Let us suppose that you do not know the methods of reading from a binary file. You could use a man page search such as

```
$ man -k binary file | grep read
```

Remember though that when you use multiple words with the -k option, they are OR-ed together, so the output includes lines with either word (or both). If you do this search, you will see a list of perhaps several dozen man pages. If you get a long list you can filter it further by limiting the output to only sections 2 or 3 of the man pages with a third stage in the pipeline:

```
$ man -k binary file | grep read | grep '([23])'
```

In this list will be the page for two prospective functions to use:

+   fread (3)      - binary stream input/output
+   pread (2)      - read from or write to a file descriptor at a given offset
+   read (2)       - read from file descriptor

The first, fread(), in Section 3, is part of the C Standard I/O Library; it is C's function for reading binary files. The second, pread(), in Section 2, is the prototype of a system call. The third, read(), in Section 2, is also the prototype of a system call. As we are primarily interested in what Unix in particular has to offer us, we will look at the system calls. We begin with read() and return to pread() later. In Chapters 5 and 7, we will revisit the C Standard I/O Library.

We want to see what the man page for read() has to say. If you do not specify the section number when you type “man read”, you will get the man page from the first section, and you will discover that there is also a UNIX command, /usr/bin/read:

```
$ man read
```

which will output the man page for the read command in Section 1. You must type

```
$ man 2 read
```

to get the man page for the read() system call. I have included the important parts of the man page below.

```
NAME
    read - read from a file descriptor
SYNOPSIS
#include <unistd.h>
```
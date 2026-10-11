```
exit(EXIT_SUCCESS);
}
```

The open statement attempts to open the file, hello, in read-only mode. O_CREAT will cause the file to be created if it does not exist but, if it does, O_TRUNC sets the file's length to zero, as if it was newly created. When the file is open, fopen promptly closes it.

In particular, note that the source code checks close's return value. Although it is common not to do so, it is also a serious programming error for two reasons. First, on a networked filesystem, such as NFS, the close call may fail due to network latency. Second, many systems are configured with write-behind caching, meaning that a write call will return successfully, but the operating system will wait to perform the actual disk write until a more convenient time. As the close(2) manual page states:

> "The error status may be reported at a later write operation, but is is guaranteed to be reported on closing the file. Not checking the return value when closing the file may lead to silent loss of data."

# Reading and Writing Files

Likely, you will want to read from, write to, and move around files. To read and write files, the following two functions are provided in unistd.h:

```
ssize_t read(int fd, void *buf, size_t count);
s size_t write(int fd, const void *buf, size_t count);
```

read attempts to read up to count bytes from the file opened on the file descriptor fd, and stores the read data into the buffer specified by buf. It returns the number of bytes read on success (0 indicates an end-of-file condition), which may be less than the bytes requested, or -1 if an error occurs, errno will be set if an error occurs. After a successful read, the file pointer will be advanced by the number of bytes read, not necessarily by count.

Similarly, write writes up to count bytes to the file descriptor fd from the buffer pointed to by buf. A successful write returns the number of bytes written (0 meaning that nothing was written). On error, write returns -1 and sets errno.

# Example

![](bbox=[0.03, 0.75, 0.11, 0.8])

# Example

The following program reads in its own source code, and then writes it out to /dev/null and to a file named /tmp/foo.bar:

```
/*
 * fread.c - The read and write system calls
```
# 18.4 Writing a File

Once a file has been opened using the open() or creat() system call, you can write to it using the write() system call. Here is a brief description of the write() call:

```
```c
#include <sys/types.h>
#include <unistd.h>

ssize_t write(int fd, const void *buf, size_t nbytes);

Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```
```

This call tries to write nbytes bytes from the main memory area pointed to by buf to the file with the file descriptor fd. The data is written starting with the current location of the read/write file pointer. Upon completion, the write() call returns the number of bytes actually written, which may be less than nbytes. The file pointer advances by the number of bytes actually written. For a regular file, the call guarantees writing nbytes if the disk is not full or the file size has not exceeded the maximum file size supported by the UNIX system. However, with other files, such as sockets (see Chapter 20), this is not guaranteed.

## TABLE 18.7 Some Common Reasons for the write() System Call to Fail

| Reason for failure | Value of errno |
| --- | --- |
| The fd argument is not a valid descriptor for writing | EBADF |
| The fd argument is associated with a negative pointer. | EINVAL |
| File size limit for the process or the maximum file size limit has reached | EFBIG |
| The file system containing the file is full. | ENOSPC |
| The user's quota of disk blocks on the file system containing the file has been exhausted. | EDQUOT |
| An I/O error occurred while reading from the file system. | EIO |
| The file reading operation is interrupted. | EINTR |
| The nbytes value is greater than INT_MAX, i.e., the maximum value of an integer. | EINVAL |

We now enhance the open_close.c program and convert it into a file copy program, cpy, with the following syntax:

```
```c
#include <fcntl.h>
#include <unistd.h>

#define SIZE 512

void closefd(int);
```
```

The program copies the source file, an existing file, to the target file, a nonexistent file. The compilation and execution of the example program shows the program output.

```
```c
% cat cpy.c
#include <fcntl.h>
#include <unistd.h>

#define SIZE 512

void closefd(int);
```
```
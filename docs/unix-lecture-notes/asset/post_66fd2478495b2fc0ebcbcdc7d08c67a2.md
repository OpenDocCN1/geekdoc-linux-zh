
## 2.8.2 Opening/Creating Files For Writing

The cp command has to create a file if it does not exist and open it for writing, or overwrite it if it does exist. To overwrite a file, it is first truncated, i.e., its length is set to 0, and then the new data is written to the empty file.

### 2.8.2.1 Creating/Truncating Files

The first task is to learn how to create files and truncate them. In fact, one call accomplishes both. The creat() system call is used to open a file for writing, if it exists, setting its length to 0 first, or if it does not exist, to create it. Notice that there is no "e" at the end of creat. If you type "man creat" you will get the man page for the open() system call:

```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
int open(const char *pathname, int flags);
int open(const char *pathname, int flags, mode_t mode);
int creat(const char *path, mode_t mode);
```

The creat() system call has two arguments, a C string and a mode_t. The string should contain the path name of the file to be created and the mode_t specifies the file's mode, i.e., its permission string, as an octal number. For example,

```
fd = creat("prototype", 0751)
```

creates a file named prototype in the current working directory, if it does not exist, with permission 0751 (owner can read, write, and execute, group can read and execute, others can execute only) provided that the process's umask does not modify the permission. Umasks are covered in the next chapter. If the file exists, the mode argument is ignored and the file is truncated. In either case, upon termination of the call, fd is a file descriptor associated with the write-only connection to the file.

### 2.8.2.2 Writing to Files

Having opened a file for writing, the next step is to write data into it. The write() system call is a symmetric counterpart to the read() call. It is used for writing sequences of bytes to the file specified by a given file descriptor:

```
#include <unistd.h>
ssize_t write(int fildes, const void *buf, size_t nbyte);
```

It is possible to prevent the file from being overwritten in case it exists, but not if you use the creat() call to try to create it. Instead the open() call must be used. Chapter 4 covers the various methods of opening a file for writing.

The `size_t` type stores the sizes of things in bytes. It is usually a typedef of an unsigned long integer, which may be 32 or 64 bits. The `ssize_t` type is almost the same as the `size_t` type. It differs only in that it is signed and that it can also store a −1. If successful, the `write()` call transfers `num_bytes` bytes from the memory location pointed to by `buf` in the process’s address space to the position of the file-pointer in the file associated with `fd`, and returns the number of bytes transferred. If the kernel cannot copy any of the data, `write()` returns −1.

The word "buffer" is used to describe the second parameter in the `read()` and `write()` system calls. It is declared as a void pointer. It is called a buffer because it is a storage location in the memory space of the calling process that is used to hold the data to be transferred to or from the file.

The code fragment

```
if (write(fd, buffer, num_bytes) != num_bytes) {
        fprintf(stderr, "Problem writing to file.\n");
}
```

attempts to transfer `num_bytes` bytes from the memory location pointed to by `buffer` to the position of the file pointer in the file opened for writing via the file descriptor `fd`. (By default, the file pointer is at “the end” of the file, unless it has been moved elsewhere.) The reason for the condition

```
if (write(fd,buffer,num_bytes) != num_bytes)
```

is that the return value of `write()` is the number of bytes actually written and it may not be equal to the number of bytes that were supposed to be written. The number of bytes successfully written may be less than `num_bytes` for any number of reasons. The file might have reached a predefined maximum size, the disk might be full, or the user’s disk quota might be reached. This is why it is necessary to compare the return value of the `write()` call with the value of its third parameter.

## 2.8.3 A First Attempt at cp

The structure of the cp command is

- open the sourcefile for reading
- open the copyfile for writing
- while a read of data from the sourcefile to a buffer is not an empty read
- write the data from the buffer to the copyfile
- close the sourcefile
- close the copyfile

We know how to open and close files and we know how to read and write them, so this is a relatively easy program for us at this point. The only points that need explanation are how we create and use buffers. For example, how big should the buffer be? How do we declare it and pass it to the calls?

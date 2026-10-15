
output of the ls -l fifo1 greeting command shows that both are empty. The output of the du fifo1 greeting command shows that both use one disk block. We put "Hello, world!" (14 bytes) in the greeting file as well as fifo1. The output of the second ls -l fifo1 greeting command shows that fifo1 is still empty, but greeting contains 14 bytes. The output of the du fifo1 greeting command shows that whereas fifo1 still uses one disk block, the greeting file uses five disk blocks. Even after we empty fifo1 using the cat fifo1 command, the disk usage of fifo1 remains unchanged. This session shows that when we put data into fifo1, the data does not go into a disk object associated with it but into the memory buffer (pipe) associated with fifo1.

```
% mkfifo fifo1
% touch greeting
% ls -i fifo1 greeting
4933 fifo1  4934 greeting
% ls -l fifo1 greeting
prw-r--r-- 1 sarwar faculty 0 Apr 18 17:29 fifo1
-rw-r--r-- 1 sarwar faculty 0 Apr 18 17:29 greeting
% du fifo1 greeting
1       fifo1
1       greeting
% cat > greeting
Hello, world!
% cat greeting > fifo1 &
[1] 68928
% ls -l fifo1 greeting
prw-r--r-- 1 sarwar faculty 0 Apr 18 17:29 fifo1
-rw-r--r-- 1 sarwar faculty 14 Apr 18 17:31 greeting
% du fifo1 greeting
1       fifo1
5       greeting
% cat fifo1
Hello, world!
[1]  + Done                    cat greeting > fifo1
% du fifo1 greeting
1       fifo1
5       greeting
%
```

The following session was captured on a Solaris machine to show that FIFOs work the same way on Solaris too. The only difference is that, whereas on a BSD system an empty FIFO uses one disk block, it does not use any disk space on Solaris, as shown in the output of the du fifo1 greeting command.

```
$ mkfifo fifo1
$ touch greeting
$ ls -i fifo1 greeting
$ ls -l fifo1 greeting
prw-r--r-- 1 sarwar faculty 0 Apr 18 17:42 fifo1
-rw-r--r-- 1 sarwar faculty 0 Apr 18 17:42 greeting
$ du fifo1 greeting
0 fifo1
1 greeting
$ cat > greeting
Hello, world!
$ cat greeting > fifo1 &
[1] 10044
$ ls -l fifo1 greeting
prw-r--r-- 1 sarwar faculty 0 Apr 18 17:42 fifo1
-rw-r--r-- 1 sarwar faculty 14 Apr 18 17:43 greeting
$ du fifo1 greeting
0 fifo1
9 greeting
$ cat fifo1
Hello, world!
[1]+ Done cat greeting > fifo1
$ du fifo1 greeting
0 fifo1
9 greeting
$
```

## EXERCISE 20.2

Replicate these shell sessions on your UNIX system(s). Do they produce the same results? If not, list the differences between the results of our sessions and your sessions.

You can use any of the mknod(), mknodat(), mkfifo(), or mkfifoat() system calls to create a FIFO. However, the mknod() and mknodat() system calls require superuser privileges. The primary purpose of these system calls is to create special files, but they can also be used to create FIFOs. The mkfifo() and mkfifoat() calls do eventually invoke the mknod() system call. Once a FIFO has been created, you can use the open(), read(), write(), and close() system calls to perform I/O with it through multiple reader and writer processes. The last process that uses a FIFO, usually a reader process, closes the FIFO and removes it from the file system using the unlink() system call. Because multiple processes can write to a FIFO, the UNIX kernel ensures that data up to PIPE_BUF bytes written by multiple processes each is written atomically and does not interleave. PIPE_BUF is defined in /usr/include/sys/param.h to be 5120 bytes on Solaris and in /usr/include/sys/syslimits.h to be 512 bytes on BSD.

channels. We primarily use the mkfifo() call in our sample programs. Here are brief descriptions of the mkfifo() and mkfifoat() system calls.

```
#include <sys/types.h>
#include <sys/stat.h>
int mkfifo(const char *path, mode_t mode);
int mkfifoat(int fd, const char *path, mode_t mode);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

The mkfifo() creates a FIFO with the name given in the path argument having access permissions specified in the mode argument. As is the case with other types of files, access permissions are restricted by the current umask. In the mkfifoat() system call, the path argument is relative to the directory associated with the file descriptor fd and not the current working directory of the user. If the fd argument is AT_FDCWD, the behavior of the mkfifoat() call is identical to the mkfifo() call.

The mkfifo() and mkfifoat() calls may fail mostly for the same reasons that the creat() and open() system calls may fail, as discussed in Section 18.8.1 and listed in Table 18.4. A few additional reasons for the failure of these calls are listed in Table 20.7.

The behavior of a FIFO that is not fully opened for I/O is similar to that of a pipe under the same condition. A write to a FIFO that no process has opened for reading results in a SIGPIPE signal to the writer process. When the last process to write to a FIFO closes it, an eof is sent to the reader process.

We now discuss a sample client-server model to illustrate the use of FIFOs for IPC between unrelated processes on the same machine. Figure 20.6 shows the algorithms for the client and server processes.

Here are the fifo.h, client.c, and server.c files that implement this client-server model.

```
% cat fifo.h
#include <string.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <sys/errno.h>
```

### TABLE 20.7 Reasons for the mkfifo() and mkfifoat() System Calls to Fail

| Reason for Failure | Value of errno |
|---|---|
| The directory under which the FIFO is to be created does not have write permission, or a component directory in the path prefix is not searchable | EACCES |
| The FIFO named in path exists | EEXIST |
| For the mkfifoat() call, the fd argument is neither AT_FDCWD nor a valid descriptor for searching and the path argument is not an absolute pathname | EBADF |
| For the mkfifoat() call, the fd argument is neither AT_FDCWD nor a valid descriptor for a directory and the path argument is not an absolute pathname | ENOTDIR |

# TABLE 20.5 The Flags for the flags Argument in the pipe2() System Call

| Flag | Meaning |
|---|---|
| O_CLOEXEC | Set the "close-on-exec" flag on the pipe descriptors. This means when a process executes an exec() system call, it does not inherit an already open pipe |
| O_NONBLOCK | Set pipe descriptors for nonblocking I/O. This means that a read() system call will not block when the pipe is empty and a write() system call will not block when the pipe is full |

The flags argument in pipe2() is used to control the attributes of the pipe descriptors. Table 20.5 describes the possible flag values.

A bitwise-OR of these values may also be used for the flags argument. When the flags argument has a value of 0, the pipe2() system call behaves like the pipe() system call.

The maximum amount of data that can reside in a pipe is dictated by the size of the pipe as a bounded buffer (i.e., the fixed-size array of characters). When a pipe is full and a writer process wants to put data into it, the writer process is blocked by the UNIX kernel. Similarly, if a pipe is empty and a reader process tries to read data from the pipe, the reader process blocks. This is known as blocking I/O through a pipe.

The amount of data a writer process can write without interruption is known as the size of an atomic write into the pipe. It is defined as PIPE_BUF in the /usr/include/sys/limits.h file under Solaris and in the /usr/include/sys/syslimits.h file under BSD. The value of PIPE_BUF is 5120 bytes under Solaris and 512 bytes under BSD. Under Solaris, you can also use the man limits command to see the meaning of each symbolic constant described in the limits.h file, including PIPE_BUF. Under BSD, you can use the limits command to display values of some of the symbolic constants defined in the limits.h file.

If multiple processes write to a pipe, then requests of PIPE_BUF bytes or less are written atomically for each process. A request to write data greater than PIPE_BUF bytes may have data interleaved, on arbitrary boundaries, with writes of other processes.

If the O_NONBLOCK flag is not set, a request to write n bytes of data may block a thread if there is not enough space in the pipe to write the requested data. However, on successful completion, the write() system call returns n.

If the O_NONBLOCK flag is set, then a write() system call never blocks and the thread continues its execution. When sufficient space is available in a pipe, a request to write PIPE_BUF bytes or less completes successfully. If sufficient space is not available, the write() system call returns -1 and errno is set to EAGAIN. If no space is available in a pipe, then a write() system call for writing more than PIPE_BUF bytes returns -1 with errno set to EAGAIN. If space is available for at least one byte, the call writes what it can and returns the number of bytes written. When the data previously written to the pipe has been read, the call writes at least PIPE_BUF bytes.

The pipe() and pipe2() calls may fail for the reasons listed in Table 20.6.
![](bbox=[0.27, 0.18, 0.73, 0.28])

Figure 8.2: Parent and child sharing a pipe.

The semantics of reading from a pipe are much more complex than reading from a file. The following table summarizes what happens when a process tries to read n bytes from a pipe that currently has p bytes in it that have not yet been read.

| Pipe Size (p) | At least one process has the pipe open for writing | No processes have the pipe open for writing |
|---|---|---|
|  | Blocking read | Non-blocking read | |
|  | At least one writer is sleeping | No writer is sleeping | blocking read | pipe open for writing |
| p = 0 | Copy n bytes and return n, waiting for data as necessary when the pipe is empty. | Block until data is available, copy it and return its size. | Return -EAGAIN. | Return 0. |
| 0 < p < n |  | Copy p bytes and return p, leaving the buffer empty. |  |  |
| p ≥ n | Copy n bytes and return n leaving p-n bytes in the pipe buffer. |  |  |  |

The semantics depend upon whether or not a writer has been put to sleep because it tried to write into the pipe previously but the pipe was full. On a non-blocking read request, if the number of bytes requested, n, is greater than what is currently in the pipe and at least one writer is in this sleeping state, then the read will attempt to read n bytes, as he pipe is emptied, the writer will be awakened to write into the pipe. If no writer is sleeping and the pipe is empty, however, then the read will block until some data becomes available.

# 8.2.1 Parent and Child Sharing a Pipe

Of course there is little reason for a process to create a pipe to write messages to itself. Pipes exist in order to allow two different processes to communicate. Typically, a process will create a pipe, and then fork a child process. After the fork, the parent and child will each have copies of the read and write-ends of the pipe, so there will be two data channels and a total of four descriptors, as shown in Figure 8.2.

On some Unix systems, such as System V Release 4 Unix, pipes are implemented in this full-duplex mode, allowing both descriptors to be written into and read from at the same time. POSIX allows only half-duplex mode, which means that data can flow in only one direction through the pipe, and
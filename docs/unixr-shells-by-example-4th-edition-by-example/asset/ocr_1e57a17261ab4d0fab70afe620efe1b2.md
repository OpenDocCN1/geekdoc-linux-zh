# Pipes.

A pipe is the oldest form of UNIX interprocess communication. A pipe allows processes to communicate with each other. It is a mechanism whereby the output of one command is sent as input to another command, with the limitation that data can only flow in one direction, normally between a parent and a child. The shell implements pipes by closing and opening file descriptors; however, instead of assigning the descriptors to a file, it assigns them to a pipe descriptor created with the pipe system call. After the parent creates the pipe file descriptors, it forks a child process for each command in the pipeline. By having each process manipulate the pipe descriptors, one will write to the pipe and the other will read from it.

To simplify things, a pipe is merely a kernel buffer from which both processes can share data, thus eliminating the need for intermediate temporary files. The output of one command is sent to the buffer, and when the buffer is full or the command has terminated, the command on the right-hand side of the pipe reads from the buffer. The kernel synchronizes the activities so that one process waits while the other reads from or writes to the buffer.

The syntax of the pipe command is

```
who | wc
```

In order to accomplish the same thing without a pipe, it would take three steps:

```
who > tempfile
wc tempfile
rm tempfile
```

With the pipe, the shell sends the output of the who command as input to the wc command; that is, the command on the left-hand side of the pipe writes to the pipe and the command on the right-hand side of the pipe reads from it (see Figure 1.9). You can tell if a command is a writer if it normally sends output to the screen when run at the command line. The ls, ps, and date commands are examples of writers. A reader is a command that waits for input from a file or from the keyboard or from a pipe. The sort, wc, and cat commands are examples of readers.

![](bbox=[0.165, 0.815, 0.885, 0.945])

Figure 1.9 The pipe.
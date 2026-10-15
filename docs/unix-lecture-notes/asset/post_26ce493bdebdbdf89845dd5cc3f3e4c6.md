
- By default, when a stream is opened, it is fully buffered, except for streams connected to terminal devices, which are line buffered.
- The buffers created by the C I/O Library are in the process's own address space, not the kernel's address space. (When your program calls a function such as printf(), the library is linked into that program; all memory that it uses is in its virtual memory.) This means that when fork() is called, the child gets a copy of the parent's library buffers, and all children get copies of these buffers. They are not shared; they are duplicated.
- The C I/O library flushes all output buffers
  - When the process tries to do output and the output buffer is full.
  - When the stream is closed.
  - When the process terminates by calling exit().
  - When a newline is written, if the stream is line buffered.
  - Whenever an input operation on any stream actually reads data from its file.
  - When fflush() is called on that buffer.
- As a corollary to the preceding statement, until the buffer has been flushed, it contains all characters that were written to it since the last time it was flushed.
- No C I/O Library function is atomic. It is entirely possible that output can be intermingled or even lost if the timing of calls by separate processes sharing a file position pointer leads to this.

Now we put these facts together. The forkdemo2 program begins with the instruction

```
printf("About to create many processes...\n");
```

If output has not been redirected, then stdout is pointed to a terminal device and it is line buffered. The string "About to create many processes...\n" is written to the terminal and removed from the buffer. When the process forks the children, they get empty buffers and write their individual messages to the terminal. Unless by poor timing a line is written over by another process, each process will produce exactly one line of output. It is quite possible that this will happen if there are a large enough number, N, of processes, as the probability of simultaneous writes increases rapidly towards 1.0 as N increases.

Let us do a bit of mathematical modeling. The printf() instruction

```
printf("Process id = %d\n", getpid());
```

writes to standard output. If the fraction of time that each process spends in the portion of the printf() function in which a race condition might occur is p, then there is a probability of 1 − (1 − p)^N that at least two processes are in that portion of code at the same time. If, for example, p = 0.05 and N = 16, then the probability of a race (and hence lost output) is 1 − 0.95^16 ≈ 0.56. If N = 32, it is 0.81 and when N = 64, it is 0.96. So you see that as the number of processes increases, it becomes almost inevitable that lines will be lost, regardless of whether they are written

to the terminal or to a different file descriptor, because the race condition is independent of how the output stream is buffered.

If standard output is redirected to a file or to a pipe, it no longer points to a terminal device and the library will fully buffer it instead of line buffering it. The block size used for buffering is much larger than the total size of the strings given to the printf() function. The consequence is that the string "About to create many processes...\n" will remain in the buffers of all child processes when they are forked, and when they each call

```
printf("Process id = %d\n", getpid());
fflush(stdout);
```

each line of the output will be of the form

```
About to create many processes...
Process id = 8810
```

and there will be twice as many lines written as there were to the terminal.

Since the command

```
forkdemo2 | wc
```

redirects the standard output of forkdemo2 to a pipe, wc will see twice as many lines as appear on the terminal. Similarly, the command

```
forkdemo2 > temp
```

redirects the standard output to a file, and the file will contain twice as many lines as what appears on the terminal.

The foregoing statement about the output to the file is true only if the executions of the printf() instructions do not overlap and no output is lost. We return to this issue shortly. The claim regarding the pipe is unconditionally true.

How can we make the behavior of the program the same regardless of whether it is to a terminal or is redirected? We can force the first string to be flushed from the buffer by calling fflush(stdout). Since there is no need to do this if it is a terminal, we can insert the two lines

```
if (!isatty(fileno(stdout)));
fflush(stdout);
```

just after the first printf().

What about the problem of lost output? How can we prevent this race condition? The answer is that we must not use the stream library but must use the lower level write() system call and file descriptors. Writes are unbuffered and we can set the O_APPEND flag on file descriptor 1 so that the race condition is eliminated. (Recall from Chapter 4 that this is how writes to the utmp file avoid race conditions.)

To use write(), we must first create the output string using the sprintf() function:

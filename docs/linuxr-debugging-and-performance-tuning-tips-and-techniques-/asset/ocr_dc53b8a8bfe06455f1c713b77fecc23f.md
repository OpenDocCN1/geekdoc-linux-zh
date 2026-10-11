then open the FIFO, write a request to it, and close it. The spooler sits in a loop, reading requests from the FIFO and processing them.

The `mkfifo()` function creates FIFO files:

```
#include <sys/types.h>            POSIX
#include <sys/stat.h>
int mkfifo(const char *pathname, mode_t mode);
```

The pathname argument is the name of the FIFO file to create, and mode is the permissions to give it, analogous to the second argument to create() or the third argument to open() (see Section 4.6, “Creating Files,” page 106). FIFO files are removed like any other, with remove() or unlink() (see Section 5.1.5.1, “Removing Open Files,” page 127).

The GNU/Linux *mkfifo*(3) manpage points out that the FIFO must be open both for reading and writing at the same time, before I/O can be done: “Opening a FIFO for reading normally blocks until some other process opens the same FIFO for writing, and vice versa.” Once a FIFO file is opened, it acts like a regular pipe; that is, it’s just another file descriptor.

The `mkfifo` command brings this system call to the command level. This makes it easy to show a FIFO file in action:

```
$ mkfifo afifo                     Create a FIFO file
$ ls -l afifo
prw-r--r--      1 arnold    devel       0  Oct 23 15:49 afifo
$ cat < afifo &                     Start a reader in the background
[1] 22100
$ echo It was a Blustery Day > afifo Send data to FIFO
$ It was a Blustery Day           Shell prompts, cat prints data
                                  Press ENTER to see job exit status
[1]+ Done             cat <afifo      cat exited
```

# ### 9.4 File Descriptor Management

At this point, the pieces of the puzzle are almost complete. fork() and exec() create processes and run programs in them. pipe() creates a pipe that can be used for IPC. What’s still missing is a way to move the pipe’s file descriptors into place as standard output and standard input for a pipeline’s producer and consumer.

The dup() and dup2() system calls, together with close(), let you move (well, copy) an open file descriptor to another number. The fcntl() system call lets you do the same thing and manipulate several important attributes of open files.
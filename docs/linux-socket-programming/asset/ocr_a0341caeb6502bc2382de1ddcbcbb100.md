(and even siblings) share the same data regions by default. The stack is the only unique region between threading tasks. Just make sure that no two people have their hands in the pot at the same time.

You can create shared memory in your processes by using the `shmget()` system call. Shared memory in this fashion sets aside a block of memory for communicating with other processes. However, this slows computation time because the process has to use the system to manage the memory access.

# Interprocess Communication (IPC)

During the poker game, the players send messages to each other and to the dealer. Some of these messages are instructional, some emotional (as you might guess). Still, the players direct the message to a particular player or to the entire group.

The tasks you design and program can use interprocess communication (IPC). IPC usually comes in the form of pipes; your task can direct messages to other tasks using these pipes. Pipes are unidirectional, like using `stdin` and `stdout` I/O channels. The system call `pipe()` creates the following pipe:

```
```
#include <unistd.h>
int pipe(int fd[2]);
```
```

The parameter `fd` is an array of two integers. You provide this array to accept the two new file descriptor references. Two common errors are

+   - `EMFILE` Too many files are already open.
- `EFAULI` `fd` is not pointing to an array of two integers.

The following is an example of using `pipe`:

```
```
/***** Example of using the pipe() system call *****/
/***** create the array to hold the descriptors *****/
int fd[2];
if (pipe(fd) != 0) /* create the pipe */
    perror("Pipe creation error");
...
read(fd[0], buffer, sizeof(buffer)); /* read from input end */
...
```
```

# NOTE

# Indexing File Descriptors

Every I/O channel is assigned a file descriptor number. This is an index into a file descriptor table. By default, every process gets three channels: `stdin` (0), `stdout` (1), and `stderr` (2). When you create a pipe, it takes the next two available slots (one for input and one for output). For example, if a task has no other files open, calling `pipe()` sets aside pipe-input (3) and pipe-output (4).
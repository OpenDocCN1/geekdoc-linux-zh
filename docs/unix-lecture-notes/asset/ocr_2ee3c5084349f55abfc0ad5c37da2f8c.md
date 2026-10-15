-a command, you will see that there are several sections of code that reside in this small pocket before the main program. There you will find the code that must be run before main() starts (what I like to call the "glue" routine), the code that runs when the program finishes, and special code for dynamic linking and relocation. When a program starts, before the operating system transfers control to the program, there are initializations and possible linking and relocation; the code there serves that purpose.

# 7.7 Creating New Processes Using fork

Now that you have a better idea of what processes actually are, we can start exploring their world. We will begin with process creation, since that is, after all, the beginning of all things.

Once the operating system has bootstrapped itself, the only way for any process to be created is via the fork() system call. All processes are created with fork():

```
#include <sys/types.h>
#include <unistd.h>
pid_t fork(void);
```

The fork() call is a hard one to accept at first; you probably have never seen a function quite like it before. It is very appropriately named, because the statement

```
pid_t processid = fork();
```

causes the kernel to create a new process that is almost an exact copy of the calling process, such that after the call, there are two processes, each continuing execution at the point immediately after the call in the executing program! So before the instruction is executed, there is a single process about to execute the instruction, and by the time it has returned, there are two. There has been a fork in the stream of instructions, just like a fork in a road. It is almost like process mitosis.

The process that calls fork() is called the parent process and the new one is the child process. They are distinguished by the values returned by fork(). Each process is able to identify itself by the return value. The value returned to the parent is the process-id of the newly created child process, which is never 0, whereas the value returned to the child is 0. Therefore, each process simply needs to test whether the return value is 0 to know who it is. The child process is given an independent copy of the memory image of the parent and the same set of resources. It is essentially a clone of the parent and is almost identical in every respect. Unlike cellular mitosis though, it is not symmetric.

The typical use of the fork() call follows the pattern

```
processid = fork();
```
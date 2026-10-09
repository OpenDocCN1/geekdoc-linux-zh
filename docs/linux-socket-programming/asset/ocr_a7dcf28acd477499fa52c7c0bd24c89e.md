# NOTE

Linux's Task Scheduling

Multitasking operating systems use many different methods for scheduling tasks. Linux uses a prioritized round robin scheduling scheme. In a round robin, each task gets a portion of the CPU time in turn. To implement priorities, this scheduling scheme moves higher priority tasks up the task list more quickly than lower ones.

# Task Differences

The differences between processes and threads are subtle. When working with them, keep the following styles and features in mind.

Processes | Threads

From the point of a successful call, there are two processes running inline. | The caller supplies the name of the function to run as the child.

The child must be explicitly terminated with an exit() system call. | The child can explicitly or implicitly terminate with a pthread_exit(void* arg) or a return statement.

No shared data. The only information passed to the child is the snapshot of the parent's data before the system call. The child shares the parent's data, accepts a parameter, and/or returns a value.

The child is always associated with the parent. When it ends, the parent must clean up the child. | The child can be detached from the parent. Thus, the child can terminate without parental intervention. (Unless the child is detached, the parent has to clean up the thread as well.)

Because each process's data is independent from the others, there is no contention for resources. | All contended data must be identified and locked so no corruption can occur.

Independent file system. | Linked file systems. The child sees any changes the parent makes to the current working directory (chdir), the root file system (chroot), or the default permissions on file creation (umask).

Shared file tables. If the child closes a file, the parent loses access to the file. | Open file tables are not shared. The operating system copies the tables so that the two processes have the same file open, but closing one channel does not affect the other process.

No shared signals. | Signals are shared. One thread can block a signal using sigprocmask() without affecting the other threads.

Use whichever fits the circumstances better and with which you are most comfortable. There are clear advantages to getting the free shared-data that threads offer, but the simplicity and independence of processes make them appealing as well.

# How Do I Create a Process?

Multitasking is most often achieved with processes. It shares nothing, creates a new instance of your program, and inherits copies of the parent's open I/O channels. To spawn a process, use the fork() system call:

```
#include <unistd.h>
pid_t fork(void);
```
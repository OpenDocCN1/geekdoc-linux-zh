
This feature becomes a signal processor. The signum parameter determines which signal is sent to the handler (the same handler can be logged for multiple signals by several `sigaction()` calls). After logging in, the handler will always be called when it receives the appropriate signal:

```c
#include <signal.h>
void sigint_handler(int signum)
{
    // SIGINT processing
}
// ...
struct sigaction action = {0};
action.sa_handler = sigint_handler;
sigaction(SIGINT, &action, 0);
```

If we need to organize the wait for the signal, the simplest way is to open a system call `pause()`. In this case, the process enters standby mode, from which it will exit on any signal:

```c
// ask the handlers for help with sigaction()
pause(); // wait for a signal
```

## Signal Generation

Let's consider how to send a process signal. This uses the `kill()` system call.

```c
#include <signal.h>
int kill(pid_t pid, // process ID
     int signum); // signal number
```

For example, sending a SIGHUP signal to a process pid that is specified at the command line:

```c
kill(atoi(argv[1]), SIGHUP);
```

## Organization of Asynchronous Execution of Processes

Consider how you can use signal processing to organize asynchronous process execution. As you know, calling `waitpid()` causes an offspring to execute synchronously. When to start the descendant process is asynchronous. It seems natural not to call `waitpid()` in the ancestor process for that descendant. But upon completion of the descendant process, it will turn into a zombie process.

To avoid this, you must take advantage of the fact that the ancestor process receives a special SIGCHLD signal at the end of the descendant process. Calling `waitpid()` in this signal handler will remove the descendant process information from the process table, leaving no zombies in the system.

```c
void clear_zombie(int signum)
{
    waitpid(-1, NULL, 0);
}
struct sigaction action = {0};
action.sa_handler = clear_zombie;
sigaction(SIGCHLD, &action, 0);
if ((pid = fork()) == -1)
    _exit();
if (pid == 0)
{
    // descendant running asynchronously
    exit();
}
else
{
    // ancestor does not have a waitpid() call
}
```

# Managing Threads in Linux

## Basic support for multithreading

Until recently, the only multithreading support for Linux was the `clone()` system call, which made it possible to create a new process based on an existing one. This call is similar to the `fork()` call but has several other features.

- For the new process, you need to specify a special set of flags that determine how resources will be distributed between the ancestor and the descendant. The resources that can be shared include address space, open file information, signal handlers. Note that in the traditional `clone()` implementation, there is no special use of process identifier (pid), ancestor ID, and some other important attributes.
- The new process probably can set a new stack (as a consequence, call `clone()`, two processes can share a common memory segment, making stack sharing unacceptable for general use).

Support for `clone()` means implementing a 1:1 multithreading scheme. The primary entities in the system are processes, not threads (in Linux, the entities managed by the kernel are called processes, not kernel threads). The traditional multithreading implementation on Linux determines that user threads are mapped to processes in the kernel. Therefore, it is impractical to look at thread data structures in Linux separately - it is displayed with the same `task_struct` structure as the process.

## The Disadvantages of Traditional Multitasking Support For Linux

Multithreading basics in the Linux kernel have not undergone fundamental changes since the `clone()` system call. In the meantime, Linux has evolved from an experimental system to an industry-wide system where enterprise-class heavy-duty applications are implemented.

This use of the system has led to the implementation of multi-threaded high reliability and scalability.

It became apparent that the `clone()` system call implementation did not meet these requirements. We had the full implementation of multithreaded processing facilities at the system level in the kernel.

Thread control is part of the standard POSIX 1996 corresponding API which was named POSIX Threads.

## Linux Kernel Threads

In addition to user processes and threads, Linux also supports a special kind of scheduled objects that are already known as kernel threads. Such threads are scheduled as normal processes and threads, each with its own id (pid). Differences of kernel threads from processes and user threads are that:

- The thread functions for them are defined in the kernel code.
- They run only in kernel mode.
- They have inaccessible areas of memory: memory allocated in user mode.

## The Thread Management Software Interface

### Creating Threads

To add a new thread to the current process, POSIX uses the `pthread_create()` function with the following syntax:

```c
#include <pthread.h>
int pthread_create(pthread_t *th, pthread_attr_t *attr,
                   void *(*thread_fun)(void *), void *arg);
```

Consider the parameters of this function:

- `th` is a pointer to a predefined structure of type `pthread_t` which will then be passed to other functions to work with threads; then call the API to handle the thread (thread handle).
- `attr` is a pointer to a structure with thread attributes (you need to pass a null pointer to use the default attributes; some attributes will be reviewed later).
- `thread_fun` is a pointer to a thread function that should be described as:

```c
void *mythread_fun(void *value)
{
    // executing the thread code
}
```

- `arg` - the data passed to the thread function (there they will get a parameter value).

An example of creating a POSIX thread:

```c
#include <pthread.h>
// thread function
void *thread_fun(void *num)
{
    printf("thread number %d\n", (int)num);
}
// ....................
pthread_t th;
// create the second thread
pthread_create(&th, NULL, thread_fun, (void *)++thread_num);
// there are two threads running in parallel
```

The new thread begins to run in parallel with the thread that created it. For example, if a thread was created inside the `main()` function, then two threads would continue to execute: an original program executing the `main()` code and a new one.

### Completion of POSIX Threads

To end a thread, just go to the end of its thread function `thread_fun()` or call `pthread_exit()` from it:

```c
#include <pthread.h>
void pthread_exit(void *retval);
```

The `retval` parameter specifies the return code. Here is an example of ending a thread:

```c
void *thread_fun(void *num)
{
    printf("thread number %d\n", (int)num);
    pthread_exit(0);
}
```

There are two different situations for the application startup code:

- Executing the `return` statement or executing all statements by the end of `main()` completes the whole process with all threads also completing their execution.
- Executing the `pthread_exit()` function inside the `main()` function completes only the initial thread; this action does not affect other threads in the program - they will continue executing until they are completed.

Calling the `pthread_exit()` function is used only to join threads because it does not release the thread resources - this is the responsibility of the thread joiner.

### Waiting For Completion Of Threads

To await completion of threads, use the `pthread_join()` function. It has the following syntax:

```c
int pthread_join(pthread_t thread, void **status);
```

This function blocks the thread where it was called until the thread specified by the handle completes its execution. If the `status` is not a null pointer, it will point to the data returned by the thread after the call (argument to `pthread_exit()`). If the thread is already complete by the time the `pthread_join()` function is called, its information should be read immediately.

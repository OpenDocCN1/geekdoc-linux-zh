The system call interface in Linux, as with most Unix systems, is provided in part by the C library. The C library implements the main API on Unix systems, including the standard C library and the system call interface. The C library is used by all C programs and, because of C's nature, is easily wrapped by other programming languages for use in their programs. The C library additionally provides the majority of the POSIX API.

From the application programmer's point of view, system calls are irrelevant; all the programmer is concerned with is the API. Conversely, the kernel is concerned only with the system calls; what library calls and applications make use of the system calls is not of the kernel's concern. Nonetheless, it is important for the kernel to keep track of the potential uses of a system call and keep the system call as general and flexible as possible.

A meme related to interfaces in Unix is “Provide mechanism, not policy.” In other words, Unix system calls exist to provide a specific function in an abstract sense. The manner in which the function is used is not any of the kernel's business.

# # Syscalls

System calls (often called *syscalls* in Linux) are typically accessed via function calls defined in the C library. They can define zero, one, or more arguments (inputs) and might result in one or more side effects,¹ for example writing to a file or copying some data into a provided pointer. System calls also provide a return value of type *long* that signifies success or error—usually, although not always, a negative return value denotes an error. A return value of zero is usually (but again not always) a sign of success. The C library, when a system call returns an error, writes a special error code into the global *errno* variable. This variable can be translated into human-readable errors via library functions such as *perror*().²

Finally, system calls have a defined behavior. For example, the system call *getpid*() is defined to return an integer that is the current process's PID. The implementation of this syscall in the kernel is simple:

```
```
SYSCALL_DEFINE0(getpid)
{
    return task_tgid_vnr(current); // returns current->tgid
}
```
```

Note that the definition says nothing of the implementation. The kernel must provide the intended behavior of the system call but is free to do so with whatever implementation

> ¹ Note the “might” here. Although nearly all system calls have a side effect (that is, they result in some change of the system's state), a few syscalls, such as *getpid*(), merely return some data from the kernel.

> ² The use of type *long* is for compatibility with 64-bit architectures.
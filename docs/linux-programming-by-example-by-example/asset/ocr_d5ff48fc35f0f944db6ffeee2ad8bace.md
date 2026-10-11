# System Call Limitations

The real system calls are optimized for speed and, in order to maintain the integrity of kernel mode code, have three significant restrictions:

+   * Each argument passed from user to kernel mode is the same length, usually the native word size of the host processor architecture.

+   * System calls always return signed integers.

+   * To minimize the size of the kernel and to keep it fast, all data passed to kernel mode is passed by reference. This is particularly important when dealing with potentially large data structures.

In reality, the first two limitations have little meaningful effect on the programs you write. The third restriction simply means that you have to use pointers to structures, rather than structures themselves, when invoking system calls.

# Why Use System Calls?

As the previous section suggested, the main reason to use system calls is to request a service from the kernel that user code cannot provide itself. What sort of system services are available? As of kernel version, 2.2.5, there were 190 system calls enumerated in the file `/usr/include/asm/unistd.h`, which contains all of the system calls and defines the relevant function calls and macros for using them. The list of available services includes the following:

+   * Process management, such as `fork`, `exec`, `setgid`, `getuid`, and so on

+   * The complete signal handling interface, such as `sigaction`, `sigsuspend`, `sigprocmask`, and `sigreturn`

+   * Filesystem services, such as `mkdir`, `chdir`, `fstat`, `read`, `write`, `open`, and `close`

+   * Memory management such as `mmap`, `munmap`, `sbrk`, `mlock`, and `munlock`

+   * Network services, including `sethostname` and `setdomainname`

+   * Process scheduling, which merely mortal programmers should never need to use

One reason you might want to use system calls is to implement your own memory management scheme for your application. As you know, the standard C library provides `malloc` for requesting memory from the operating system. What you may not realize, however, is that you can create your own `malloc` using the `brk` and `sbrk` system calls (`brk` and `sbrk` manipulate a program's data space). This would perhaps remedy some of the standard
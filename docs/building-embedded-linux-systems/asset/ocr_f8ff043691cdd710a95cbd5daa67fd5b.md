The first decision facing a builder of a new toolchain, therefore, is which C library to use. Because the C library is a component in both the toolchain (both as part of the compiler, for support of C++ and other languages, and in the form of library headers) and the runtime image (the code library itself and the allocation code that is compiled to use it), it is impossible to change this decision later without affecting the entire system.

# The threading library

Threads are a popular modern programming technique involving several independent, asynchronous tasks residing in the same process address space. The Linux kernel, prior to the 2.6 series, provided very little support for threads. To fill the gap, a few different threading libraries were developed that implemented much of the required support in user space with minimal kernel assistance. The most common was the LinuxThreads library, which was an implementation of the POSIX Threads standard and was distributed as a glibc add-on until Linux version 2.5. LinuxThreads was a noble and useful project, but it suffered from problems with scalability and adherence to standards, due to limitations imposed by the weakness of support for threads in the Linux kernel at that time. For example, both the getpid() system call and signal handling in LinuxThreads are non-compliant vis-à-vis the POSIX standard, on account of kernel-imposed limitations.

The release of the Linux 2.6 series was accompanied by a new thread implementation called the New POSIX Threading Library (NPTL). NPTL relies on Linux kernel supports for threads. A key piece of the implementation, known as a fast user space mutex (futex), provides a robust, POSIX-compliant threading implementation that scales up to thousands of threads. NPTL is now the supported Linux threading library and is distributed as part of recent versions of glibc.

For any new project making use of recent kernel versions and glibc releases, NPTL is the threading library of choice. However, because all Linux glibc releases prior to 2.6.16 contain bugs affecting the threading library, and because it is not unheard of for embedded system builders to base systems on older kernel and glibc releases (mainly due to vendor support issues), LinuxThreads can still be a valid option, especially if your system is only expected to make very limited use of threads.

You can also start off with LinuxThreads and migrate to NPTL, because both conform (at least roughly) to the POSIX standard.

The conftstr() function can be used to test which threading library implementation is in use at runtime:

```
```c
#define _XOPEN_SOURCE
#include <unistd.h>
#include <stdio.h>

int main(void)
{
```

```
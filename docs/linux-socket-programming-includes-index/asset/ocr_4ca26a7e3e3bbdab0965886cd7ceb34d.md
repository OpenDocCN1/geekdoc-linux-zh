If you get any error from a `fork()` system call, you may have problems with your process table or memory resources. One symptom of an overburdened operating system is being denied resources. Memory and process table entries are foundational to a properly functioning OS. Because these resources are so important, Linux limits the total amount of resources a process can have. When you can’t get a reasonably sized chunk of memory or you can’t create a new task, you may have problems with your program or you don’t have enough memory.

# How Do I Create a Thread?

Threads offer you the power of closely shared resources between parent, children, and siblings. Use threading to delegate data tasks for a common goal. For example, one thread retrieves a picture, while another converts it for display. In contrast, processes help you when you don’t need such closely connected interactions.

One specific implementation of threading you may have heard about is Pthreads. Pthreads is a set of library calls that offer threading in a POSIX 1c-compliant way. The programs you write using Pthreads are likely to be compatible with other POSIX-compliant operating systems. The library call for creating new Pthreads is `pthread_create()`:

```
```
#include <pthread.h>
int pthread_create(pthread_t* child, pthread_attr_t* attr, void*
*(*fn)(void*), void* arg);
```
```

> **The Difference Between Library and System Calls**
> 
> The difference between a library call and a system call is the amount of work done in libraries versus the kernel. A `fork()` system call really is an interface into the kernel system services. The `pthread_create()` is in a different library that translates the call into the `clone()` system call. In this case, to compile C programs with threads, be sure to include _-lpthread_ at the last argument on the `cc` command line. For example, to compile *mythreads.c* and link it with the Pthreads library, use the following:
> 
> ```
> cc mythreads.c -o mythreads -lpthreads
> ```

As with the `fork()` system call, at the point you successfully execute `pthread_create()`, you have another task running. However, creating threads is more complicated than the `fork()` system call. Depending on how many features you want to use, you may have to do more preparatory work. Each parameter provides the materials needed to start the new thread (see Table 7.1).
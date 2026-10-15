
# Chapter 1　Introduction to System Programming

> > “UNIX is basically a simple operating system, but you have to be a genius to understand the simplicity.” - Dennis Ritchie, 1941 - 2011.

## Concepts Covered

- The kernel and kernel API,
- System calls and libraries,
- Processes, logins and shells,
- Environments, man pages,
- Users, the root, and groups,
- Authentication,
- File system, file hierarchy,
- Files and directories,
- Device special files,
- UNIX standards, POSIX,
- System programming,
- Terminals and ANSI escape sequences,
- History of UNIX,
- syscall, getpid, ioctl

## 1.1　Introduction

A modern software application typically needs to manage both private and system resources. Private resources are its own data, such as the values of its internal data structures. System resources are things such as files, screen displays, and network connections. An application may also be written as a collection of cooperating threads or sub-processes that coordinate their actions with respect to shared data. These threads and sub-processes are also system resources.

Modern operating systems prevent application software from managing system resources directly, instead providing interfaces that these applications can use for managing such resources. For example, when running on modern operating systems, applications cannot draw to the screen directly or read or write files directly. To perform screen operations or file I/O they must use the interface that the operating system defines. Although it may seem from the C standard library such as `getc()` or `printf()` access files directly, they do not; they make calls to system routines that do the work on their behalf.

The interface provided by an operating system for applications to use when accessing system resources is called the operating system’s *application programming interface (API)*. An API typically consists of a collection of function, type, and constant definitions, and sometimes variable definitions as well. The API of an operating system in effect defines the means by which an application can utilize the services provided by that operating system.

It follows that developing a software application for any *platform* requires mastery of that platform’s API. Therefore, aside from designing the application itself, the most important task for the application developer is to master the system level services defined in the operating system’s API. A program that uses these system level services directly is called a *system program*, and the type of programming that uses these services is called *system programming*. System programs make requests for resources and services directly from the operating system and may even access the system

¹We use the term platform to mean a specific operating system running on a specific machine architecture.

resources directly. System programs can sometimes be written to extend the functionality of the operating system itself and provide functions that higher level applications can use.

These lecture notes specifically concern system programming using the API of the UNIX operating system. They do not require any prior programming experience with UNIX. They also include tutorial information for those readers who have little experience with UNIX as a user, but this material can be skipped by the experienced UNIX users.

In the remainder of these notes, a distinction will be made between the user’s view of UNIX and the *programmer’s view* of UNIX. The user’s view of UNIX is limited to a subset of commands that can be entered at the command-line and parts of the file system. Some commands and files are not available to all users, as will be explained later. The programmer’s view includes the programming language features of the kernel API, the functions, types, and constants in all of the libraries, the various header files, and the various files used by the system. Familiarity with basic C programming is assumed.

```c
#include <stdio.h>
/* copy from stdin to stdout */

int main()
{
    int c;
    while ( ( c = getchar() ) != EOF )
        putchar(c);
    return 0;
}
```

![](img/edd55012c780b4e999320d08ab27959e_1_0.png)

*Figure 1.1: Simple I/O model used by beginning programmer.*

## 1.2  A Programming Illusion

A beginning programmer typically writes programs that follow the simple I/O model depicted in Figure 1.1: the program gets its input from the keyboard or a disk file, and writes its output to the display screen or to a file on disk. Such programs are called *console applications*, because the keyboard and display screen are part of the console device. Listings 1.1 and 1.2 contain examples of such a program, one using the C Standard I/O Library, and the other, the C++ stream library. Both get input from the keyboard and send output to the display device, which is some sort of a console window on a monitor.

The comment in Listing 1.1 states that the program copies from stdin to stdout. In UNIX, every process has access to abstractions called the standard input device and the standard output device. When a process is created and loaded into memory, UNIX automatically creates the standard input and standard output devices for it, opens them, and makes them ready for reading and writing respectively. In C (and C++), stdin and stdout are variables defined in the <stdio.h>

¹In fact, every POSIX-compliant operating system must provide both a standard input and standard output stream.
²It also creates a standard error device that defaults to the same device as standard output.

# Chapter 1　Introduction to System Programming

> > “UNIX is basically a simple operating system, but you have to be a genius to understand the simplicity.” - Dennis Ritchie, 1941 - 2011.

# Concepts Covered

+   The kernel and kernel API,
+   System calls and libraries,
+   Processes, logins and shells,
+   Environments, man pages,
+   Users, the root, and groups,
+   Authentication,
+   File system, file hierarchy,
+   Files and directories,

+   Device special files,
+   UNIX standards, POSIX,
+   System programming,
+   Terminals and ANSI escape sequences,
+   History of UNIX,
+   syscall, getpid, ioctl

# 1.1　Introduction

A modern software application typically needs to manage both private and system resources. Private resources are its own data, such as the values of its internal data structures. System resources are things such as files, screen displays, and network connections. An application may also be written as a collection of cooperating threads or sub-processes that coordinate their actions with respect to shared data. These threads and sub-processes are also system resources.

Modern operating systems prevent application software from managing system resources directly, instead providing interfaces that these applications can use for managing such resources. For example, when running on modern operating systems, applications cannot draw to the screen directly or read or write files directly. To perform screen operations or file I/O they must use the interface that the operating system defines. Although it may seem from the C standard library such as `getc()` or `printf()` access files directly, they do not; they make calls to system routines that do the work on their behalf.

The interface provided by an operating system for applications to use when accessing system resources is called the operating system’s *application programming interface (API)*. An API typically consists of a collection of function, type, and constant definitions, and sometimes variable definitions as well. The API of an operating system in effect defines the means by which an application can utilize the services provided by that operating system.

It follows that developing a software application for any *platform* requires mastery of that platform’s API. Therefore, aside from designing the application itself, the most important task for the application developer is to master the system level services defined in the operating system’s API. A program that uses these system level services directly is called a *system program*, and the type of programming that uses these services is called *system programming*. System programs make requests for resources and services directly from the operating system and may even access the system

¹We use the term platform to mean a specific operating system running on a specific machine architecture.
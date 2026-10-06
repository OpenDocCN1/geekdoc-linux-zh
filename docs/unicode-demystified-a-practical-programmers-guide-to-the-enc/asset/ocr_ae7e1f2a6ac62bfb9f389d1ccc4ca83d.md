# Programming Tools 16

With its rich set of languages and development tools, the GNU/Linux operating system provides an outstanding environment for programming. C is one of the most popular system programming languages to use with GNU/Linux, in part because the operating system itself is written mostly in C. Using C, programmers can easily access system services using function libraries and system calls. In addition, variety of tools can make the development and maintenance of programs easier.

his chapter explains how to compile and link C programs. It introduces the GNU gdb debugger and tools that provide feedback about memory, disk, and CPU resources. It also covers some of the most useful software development tools: the make utility and two source code management systems, the Revision Control System (RCS) and the Concurrent Versions System (CVS). The make utility helps you keep track of which modules of a program have been updated and helps to ensure that when you compile a program, you use the latest versions of all program modules. Source code management systems track the versions of files involved in a project.

# Programming in C

One of the main reasons the GNU/Linux system provides an excellent C programming environment is that C programs can easily access the services of the operating system. The system calls—the routines that make operating system services
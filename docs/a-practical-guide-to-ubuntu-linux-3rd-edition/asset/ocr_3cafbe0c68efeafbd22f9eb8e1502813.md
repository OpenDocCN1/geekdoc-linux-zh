![](bbox=[0.2, 0.09, 0.94, 0.3])

Figure 1-1 A layered view of the Linux operating system

year the standard was published). Ten years later the C99 standard was published; it is mostly supported by the GNU Project’s C compiler (named gcc. The original version of the language is often referred to as Kernighan & Ritchie (or K&R) C, named for the authors of the book that first described the C language.

Another researcher at Bell Labs, Bjarne Stroustrup, created an object-oriented programming language named C++, which is built on the foundation of C. Because object-oriented programming is desired by many employers today, C++ is preferred over C in many environments. Another language of choice is Objective-C, which was used to write the first Web browser. The GNU Project’s C compiler supports C, C++, and Objective-C.

# OVERVIEW OF LINUX

The Linux operating system has many unique and powerful features. Like other operating systems, it is a control program for computers. But like UNIX, it is also a well-thought-out family of utility programs (Figure 1-1) and a set of tools that allow users to connect and use these utilities to build systems and applications.

# LINUX HAS A KERNEL PROGRAMMING INTERFACE

The Linux kernel—the heart of the Linux operating system—is responsible for allocating the computer’s resources and scheduling user jobs so each one gets its fair share of system resources, including access to the CPU; peripheral devices, such as hard disk, DVD, and CD-ROM storage; printers; and tape drives. Programs interact with the kernel through system calls, special functions with well-known names. A programmer can use a single system call to interact with many kinds of devices. For example, there is one write() system call, rather than many device-specific ones.
# 5.3. INPUT/OUTPUT

The hardware emulation is sufficiently complete that MS Windows $3.1^{7}$ has been run under Linux.

# WINE

By contrast, WINE does not rely on a virtual machine system. One could say that it is a “virtual system kernel” because application programs cannot tell if they are running on MS Windows or WINE.

It still needs to operate in privileged mode, but it has the advantage that a well-behaved program does not attempt to execute privileged instructions. Instead, user programs execute a trap instruction, much like a Linux program system call. As a result, WINE merely has to slide in between the user program and the Linux kernel. It then maps user program requests into the appropriate Linux kernel calls.

# Executor

In contrast, the Executor program is not a virtual machine environment because it doesn’t use an architecture to emulate itself. Instead it qualifies as a system emulator which offers sufficient fidelity to support most every application which runs on a Macintosh. See the web$^{8}$ or ftp$^{9}$ sites for details.

# 5.3 Input/Output

The programmer’s view of Linux system I/O is given by the system calls an application program can make. Although the documentation on these calls refer to “files”, the named objects can be regular files, directories, symbolic links, block special devices, character special devices, sockets, and fifos.

A regular file is an abstraction which gives a name to a collection of data typically stored on a disk. In addition to the **read** and **write** system calls which are used to access the data, programs use **open**, **close**, **lseek**, **creat**, **link**, and **unlink** to manipulate the files.



141
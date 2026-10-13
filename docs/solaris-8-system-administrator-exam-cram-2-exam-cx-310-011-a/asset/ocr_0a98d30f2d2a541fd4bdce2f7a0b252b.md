This chapter covers some basic concepts of the Solaris 8 operating system. The first section briefly summarizes the new features of Solaris 8. The second section addresses the structure and components of the operating system. The next section summarizes the three shells, and the last section provides an overview of the online reference manual. This chapter covers the *System Concepts* test objectives.

# New Features of Solaris 8

The following enhancements have been added to the latest release of Solaris:

+   - **Internet Protocol version 6 (IPv6)**—The next generation of IP, which overcomes many of the limitations associated with the current version of IP (version 4). The main advantages are a larger address space and the auto-configuration of addresses. In Solaris 8, the network interfaces can be configured simultaneously for both IPv4 and IPv6.

+   - **Java 2 Software Development Kit (SDK)**—The latest version of the Java SDK makes Solaris a powerful platform for machine-independent software development.

+   - **Universal Disk Format (UDF) file system**—Allows easy interchange of data stored on CD-ROMs, DVDs, hard disks, and floppy disks.

+   - **Graphical wizards**—A couple of new graphical wizards have been added to improve system usability. Most notable are the Installation Wizard and the DCHP Manager. In addition, the X Server that supports X applications has been upgraded to the X11R6.4 industry standard.

# The Three Parts of the Operating System

Solaris 8, like all variations of the Unix operating system, consists of three parts: the kernel, the shells, and the file systems. Each is discussed in the next few sections.

# The Kernel

The *kernel* is a collection of software that manages the physical and logical resources of the computer. These management services include controlling the allocation of memory and other storage devices, controlling access to
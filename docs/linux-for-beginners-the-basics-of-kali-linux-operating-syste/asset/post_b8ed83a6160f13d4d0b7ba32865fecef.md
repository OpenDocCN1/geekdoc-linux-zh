
## UNIX File System Structure

Every UNIX file system has a unique root or root origin represented by /. Under this directory, you will find all the files that the operating system can access. These files are organized in different directories whose mission and name are standard for all Unix systems.

- /: Root of the file system
- /dev: Contains system files representing the devices that are physically installed in the computer
- /etc: This directory is reserved for system configuration files

In this directory, no binary files (programs) should appear. Under this, two other subdirectories should appear:

- /etc/X11: X Window configuration files
- /etc/skel: Basic configuration files that are copied to the user's directory when one is created new
- /lib: Contains the libraries needed to run programs that reside in /bin (not libraries of user programs)
- /proc: Contains special files that either receive or send information to the system kernel (It recommends not modifying the contents of this directory and its files)
- /sbin: Contains programs that are only accessible to the superuser or root
- /usr: This is one of the most important directories of the system since it contains the usage programs common to all users. Its structure is usually similar to the following:
  - /usr/X11R6: Contains the programs to run X Window
  - /usr/bin: General purpose programs, which includes the C/C++ compiler
  - /usr/doc: General system documentation
  - /usr/etc: General configuration files
  - /usr/include: C/C++ header files (.h)
  - /usr/info: GNU information files
  - /usr/lib: General libraries of the programs
  - /usr/man: Manuals accessible with the man command
  - /usr/sbin: System administration programs
  - /usr/src: Source code of programs

In addition to the previous ones, there are other directories that are usually located in the /usr directory, such as the folders of the programs that are installed in the system.

- /var: This directory contains temporary information about the programs (which does not imply that you can delete its content; in fact, it should not be done)

## Chapter 1: Basic Operating System Concepts

### The Concept Of The Operating System, Its Purpose, And Function

#### The Concept of An Operating System

The main idea and start of our modern day operating systems was the need to create ISG including them in the use of computer systems (By *computer cybernetic system*, we mean a set of hardware and software). The computer cybernetic system initially developed for liability solutions and practical problems of users. Because it was difficult to do this with hardware alone, applications were created. These programs required general operations of hardware management, distribution of hardware from resources, and the like. These operations are grouped under a separate layer of software, which is known as the operating system.

Further, the capabilities of operating systems went far beyond the basic set of operations required by applications, but the intermediate position of such systems between applications and hardware remained unchanged.

#### Purpose Of The Operating System

Operating systems provide us with a score of cybernetic system, and secondly, efficiency and reliability of its work. The first function is characteristic of the OS as an extended machine, the second - the OS as a distributor of hardware resources.

#### Operating System As An Extended Machine

Using the operating system, the application programmer (and through his programs and the user) should have the impression that they are working with an advanced machine. The hardware is not well adapted for direct use in applications. For example, if you consider working with I/O devices at the command level of the respective controllers, you can see that the set of such commands is limited, and for many devices - primitive. The operating system hides such a hardware interface but instead offers the programmer an application programming interface that uses higher-level concepts (called abstractions).

For example, when working with a disk, a typical abstraction is a file. It is easier to work with files than directly with a disk controller (no need to consider moving the drive heads, starting and stopping the motor, etc.), as a result, the programmer can focus on the essence of his application. The operating system is responsible for interacting with the disk controller.

Abstraction highlighting makes it easy for OS and application code to change when migrating to new hardware. For example, if you install a new type of disk device on your computer (provided that it is supported by the OS), all its features will be taken into account at the OS level, and applications will continue to use the files as before. This characteristic of the system is called hardware independence. OS can be said to provide a hardware-independent environment for executing applications.

#### Operating System As A Resource Allocator

The operating system must allocate resources efficiently. It acts as the manager of these resources and provides them to applications on demand. There are two main types of resource allocation. In the case of the *spatial distribution*, resource access will be for multiple customers simultaneously, and each one of them can use the resources (the shared memory). In the case of *temporal distribution*, the system queues and, according to it, allows them to use the entire resource for a limited time (so the processor is distributed in single-processor systems).

When allocating resources, the OS resolves possible conflicts, prevents unauthorized access of programs to those resources, on which they have no rights, ensures the efficient operation of the computer system.

#### Classification Of Modern Operating Systems

Consider the classification of modern operating systems, depending on their scope. First of all, note the OS of *large* computers (mainframes). The main characteristic of the hardware for which they are designed is the performance of I/O: large computers provide a large number of peripherals (disks, printers, terminals, etc.). Such a computer cybernetic system is used for the reliable processing of large amounts of data. This OS should effectively support this process (in batch mode or time allocation). An example of an OS of this class would be IBM's OS/390.

The following category includes *server* operating systems. The main feature of such operating systems is the ability to serve a large number of user requests for shared resources. Network support plays an important role for them. There are specialized server Oses that exclude elements that are not related to the performance of their basic functions (for example, support for user applications). Universal servers (UNIX or Windows XP systems) are now more commonly used to implement servers.

The most massive category is *personal* OS. Some operating systems in this category, developed with the expectation of the user (Windows 95/98/Me) by Microsoft are simplified versions of the universal OS. Particular attention in the personal OS is given to the support of the graphical user interface and multimedia technologies. There is also a *real-time* OS. In such a system, each operation must be guaranteed to be performed within a specified time range. Real-time OS can control the flight of a spaceship, process or video demonstration. There are specialized real-time OSes such as QNX and VxWorks.

Another category is *embedded* OS. These include managing applications for various microprocessor systems used in military technology, consumer electronics systems, smart cards, and other devices. Such systems pose special requirements: placing a small amount of memory and support for specialized OS devices. Often, built-in OS is developed for a specific device; universal systems include embedded Linux and Windows CE.

### Functional Components Of Operating Systems

An operating system can be considered as a set of components, each of which is responsible for the implementation of a specific function of the system. Consider the most important features of the modern OS and the components that implement them.

The way the system is built from components and their relationship is determined by the architecture of the operating system. Each operating system is going to be a bit different in the kind of work that it can handle, and its organizational structure, so learning this and how to put it all together can be important.

### Process And Flow Management

As we mentioned, one of the most important functions of OS is to execute applications. Code and application data is stored in the computer cybernetic system on disk in a special executable manner. After the user decides to run either OS to perform a file system creates the basic unit of a computer, called a process. You can specify the following: a process is a program that executes it.

The operating system allocates resources between processes. These resources include CPU time, memory, devices, disk space as files. For the allocation of memory of each process, undertake its address space - set address memory, which allows you access. The process space is stored in the address space. The allocation of disk space for each process formed a list of open files similarly.

The processes protect the resources they possess. For example, the process address space cannot be accessed directly from other processes (it is secure), and when working with files, a mode can be

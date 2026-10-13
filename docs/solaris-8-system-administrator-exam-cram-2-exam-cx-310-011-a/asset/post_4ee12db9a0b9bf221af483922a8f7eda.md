
Likewise, if you want to find the training and certification downloads, try a search string such as this:

```
"training and certification" AND "download page"
```

Finally, don't be afraid to use general search tools such as **http://www.search.com**, **http://www.altavista.com**, or **http://www.excite.com** to search for related information. Even though Sun offers information about its certification exams online, there are plenty of third-party sources of information, training, and assistance in this area that do not have to follow a party line, as Sun does. The bottom line is this: If you can't find something where the book says it lives, start looking around. If worse comes to worse, you can always e-mail me! I just might have a clue. My e-mail address is **solaris@unixcert.net**.

![](img/b957f979417d9f16274c2eb52c8f2c9f_49_0.png)

## System Concepts

### Terms you’ll need to understand:

- Kernel
- Shell
- File system
- Daemon
- *The Solaris 8 Reference Manual*

### Techniques you’ll need to master:

- Distinguishing between the parts of the operating system
- Distinguishing between the three shells
- Using the **man** command to view online manual pages

This chapter covers some basic concepts of the Solaris 8 operating system. The first section briefly summarizes the new features of Solaris 8. The second section addresses the structure and components of the operating system. The next section summarizes the three shells, and the last section provides an overview of the online reference manual. This chapter covers the *System Concepts* test objectives.

## New Features of Solaris 8

The following enhancements have been added to the latest release of Solaris:

- **Internet Protocol version 6 (IPv6)**—The next generation of IP, which overcomes many of the limitations associated with the current version of IP (version 4). The main advantages are a larger address space and the auto-configuration of addresses. In Solaris 8, the network interfaces can be configured simultaneously for both IPv4 and IPv6.

- **Java 2 Software Development Kit (SDK)**—The latest version of the Java SDK makes Solaris a powerful platform for machine-independent software development.

- **Universal Disk Format (UDF) file system**—Allows easy interchange of data stored on CD-ROMs, DVDs, hard disks, and floppy disks.

- **Graphical wizards**—A couple of new graphical wizards have been added to improve system usability. Most notable are the Installation Wizard and the DHCP Manager. In addition, the X Server that supports X applications has been upgraded to the X11R6.4 industry standard.

## The Three Parts of the Operating System

Solaris 8, like all variations of the Unix operating system, consists of three parts: the kernel, the shells, and the file systems. Each is discussed in the next few sections.

### The Kernel

The *kernel* is a collection of software that manages the physical and logical resources of the computer. These management services include controlling the allocation of memory and other storage devices, controlling access to peripheral devices (input/output), and controlling the scheduling and execution of processes or tasks. For the most part, these services are transparent to the user. The user issues a request to perform a task, and the kernel deals with the complexity of the underlying hardware and allocating logical resources to accomplish the task.

The physical resources are controlled by means of software modules, referred to as *device drivers*, which understand how to communicate with hardware devices and control their operation. Typically, each device has a unique driver that is supplied with the hardware and identified by hardware manufacturer, model, and sometimes hardware version.

The logical resources include processes and memory. A *process* is a task or program. The kernel maintains internal data structures that define and control the processes; it also controls scheduling, executing, and terminating processes. Other important kernel services are memory management and interprocess communication. Memory management involves keeping track of available memory, allocating it to processes as needed, and reclaiming it as processes release it or terminate. *Interprocess communication* involves handling the cooperative communication between processes.

The Solaris 8 kernel supports multiple users, each of which can be executing one or more processes or tasks. Therefore, Solaris 8 is both a *multiuser* and a *multitasking* system. The Solaris 8 kernel accomplishes this level of support by allowing a task to have access to system resources for a small slice of time. A task is allowed to execute for one or more time slices and then is suspended so that another task can have access to those resources. This approach provides time-sharing among all active tasks and gives the appearance that all tasks are running simultaneously. A task that appears to be executing all the time (and typically provides a service on demand) is referred to as a *daemon*.

### The Shell

The *shell* is a software module that provides the interface between users and the kernel. It accepts user requests and submits them to the kernel. It also accepts status information and data from the kernel and presents them to the user. Typically, the shell accepts user input from a terminal or network connection; however, input can be taken from a file, a device, or even another process. In addition, output from the kernel is typically sent to the user’s terminal or network connection. Likewise, this output can be redirected to a file, a device, or another process.

The shell also provides a built-in programming language that can be used to automate repetitive tasks. This automation includes flow control and the ability to manipulate numeric and string data.

Solaris 8 provides several different shells, each with unique strengths. Some shells provide a history/recall mechanism that enables the user to reexecute a previous command by entering a few control sequences instead of reentering the command. Other shells provide built-in math manipulation.

### The File System

A *file* is a group of bytes treated as a unit for storage, retrieval, and manipulation. The *file system* is a collection of files stored on a disk drive in a hierarchical structure. A special type of file, called a *directory*, serves as a folder and is used to organize files. A file system can be thought of as an inverted tree, with the directories being the branches and the files being the leaves. The name for the top-level directory of a Unix system, *root*, comes from this analogy.

The Unix operating system supports the file system concept by providing utilities to create, mount (make accessible), check, repair, duplicate, and back up file systems. The storage space that is accessible on a Unix system is usually divided into multiple file systems. This division makes maintenance easier and improves performance.

## The Three Most Common Shells

The Solaris 8 environment provides several shells. The three most common are the Bourne shell (sh), the C shell (csh), and the Korn shell (ksh).

The Bourne shell, developed by Steven Bourne at AT&T Bell Laboratories, was the shell provided with the original Unix operating system. Ken Thompson and Dennis Ritchie designed and developed the Unix operating system at Bell Labs during the 1970s.

![](img/b957f979417d9f16274c2eb52c8f2c9f_52_0.png)

The Bourne shell is the default shell for the Solaris 8 operating system.

The C shell, developed by Bill Joy of the University of California, Berkeley, was provided with a version of the Unix operating system that was developed at the university and referred to as Berkeley Software Distribution (BSD) Unix.

The Korn shell, designed and developed by David G. Korn at AT&T Bell Laboratories, was derived from the Bourne shell by adding many features from the C shell along with new features of its own. Table 2.1 compares the features of the three shells.

![](img/b957f979417d9f16274c2eb52c8f2c9f_53_0.png)

Use of the initialization files for each shell is an important concept that is useful when you’re setting up user accounts on a Solaris 8 system. Be sure that you understand their usage and associate the filenames correctly with the appropriate shells.

**Table 2.1  Features of Solaris 8 Shells**

| Feature | sh | csh | ksh | Function |
|---|---|---|---|---|
| Aliasing | No | Yes | Yes | Lets you assign a short, simple name to a complex string and then use the name in place of the string in commands. Doing so gives the appearance of being able to add custom commands to the shell. |
| Bourne shell–compatible syntax | Yes | No | Yes | Because the Korn shell is an enhanced version of the Bourne shell, they use the same syntax. The C shell was developed separately, and its syntax is based on the C programming language. |
| Default prompt | $ | % | $ | The default prompt for both the Bourne and the Korn shells is the dollar sign ($) character, whereas the default prompt for the C shell is the system hostname followed by the percent (%) character. |
| History capability | No | Yes | Yes | The history capability of the C and the Korn shells keeps track of a user-defined number of previous commands. Instead of reentering a command, you can copy it from the history and then execute it. |
| History editing | No | Yes | No | Lets you modify and then reuse previous commands. |

*(continued)*

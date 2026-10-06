
Fedora systems, look in the /usr/share/doc/samba-*/htmldocs directory for some excellent documentation you can read from your Web browser. In particular, refer to the Samba-HOWTO-Collection/diagnosis.html file for help with troubleshooting.

# Summary

By providing centralized file servers, an organization can efficiently share information and applications with people within the organization, with customers, or with anyone around the world. Several different technologies are available for making your Linux computer into a file-serving powerhouse.

The Network File System (NFS) protocol was one of the first file server technologies available. It is particularly well suited for sharing file systems among Linux and other UNIX systems. NFS uses standard mount and umount commands to connect file systems to the directory structures of client computers.

The Samba software package that comes with many Linux distributions (or can be easily installed if it doesn't) contains protocols and utilities for sharing files and printers among Windows and OS/2 operating systems. It uses SMB protocols that are included with all Microsoft Windows systems and therefore provides a convenient method of sharing resources on LANs containing many Windows systems.

# Programming in Linux

## In This Part

- **Chapter 28** Programming Environments and Interfaces
- **Chapter 29** Programming Tools and Utilities

# Programming Environments and Interfaces

# CHAPTER 28

## In This Chapter

- Developing applications for Linux
- Using graphical programming environments
- Using command-line programming environments
- Programming for GUI interfaces
- Programming for command-line interfaces
- Using application programming interfaces

You can slice and dice the topic of Linux programming environments and interfaces in a variety of ways. For example, a list of the programming languages known to have compilers that target or run on Linux easily runs to three single-spaced, typewritten pages. You could also examine the literally hundreds of programming libraries that exist for Linux. Alternatively, you can organize the discussion into three categories: graphically oriented interfaces, command-line interfaces, and other environments.

To readers, a "programming environment" means a graphical, point-and-click integrated development environment (IDE) like that provided by Borland's Kylyk or IBM's Visual Age. Yet another way to approach the subject is to look at Linux development support for certain academic and computing subjects, such as graphics, databases, mathematics, engineering, chemistry, text processing, physics, biology, astronomy, networking, and parallel computing.

Unfortunately, there's no single definitive taxonomy on which everyone agrees, so this chapter takes the easy way out and divides things into environments and interfaces. For the purposes of this chapter, a programming environment refers to the setting in which programming takes place and the accompaniment with which someone performs programming tasks.

# Understanding Programming Environments

Conventionally understood, a programming environment is either graphical or command-line-oriented. However, the Linux programming environment also consists of the resources and capabilities provided by the system itself, that is, by the kernel and the core system components. Whether you use a mouse-driven IDE or a text editor and make, Linux imposes certain requirements and provides a number of capabilities that define the code you write in an IDE or do and can.

In this chapter, the term programming interface refers to the rules and methods followed to accomplish a particular task. As with programming environments, programming interfaces are usually thought of as graphical or command-line:

- Graphical interface — Uses the X Window System to receive and process input and information.
- Command-line interface— A strictly text-based affair that does not require a windowing system.

For example, Firefox, a web browser, has a graphical interface; it won't work if X isn't running. Pine, a popular e-mail client, has a command-line interface; it works if X is running or not.

There is a third type of interface, however, an application programming interface, or API. An API provides a structured method to write a program that performs a certain task. For example, to write a program that plays sounds, you use the sound API; to write a program that communicates over a TCP/IP network, you use the socket API. Neither playing a sound nor communicating over a TCP/IP network necessarily requires a graphical or command-line interface; both graphical and command-line programs can play sounds or over TCP/IP, provided they use the proper API.

# Using Linux Programming Environments

Linux boasts arguably the richest programming environment of any operating system currently available. As mentioned earlier, this chapter uses the term "programming environment" to describe the tools used to write computer programs on a Linux system and to refer to underlying services that make programming on a Linux system possible (or, perhaps, worthwhile).

This section looks first at the fundamental services and capabilities that inform and constrain programming on a Linux system. Next, you examine a few of the most popular graphical IDEs for creating programs on a Linux system. The section closes with a look at some of the command-line tools used for writing programs.

# Chapter 28 ◆ Programming Environments and Interfaces 755

As you will discover, some of the graphical IDEs provide comfortable editors for writing code, drawing dialog boxes, and navigating the file system, but use the command-line tools to do the work of compiling code, hiding the command-line tools beneath an attractive interface.

# The Linux Development Environment

The Linux development environment consists of the services and capabilities provided by the kernel and core system components. These services and capabilities define and limit how we write programs that run on a Linux system.

Consider files and the file system. Linux, unlike the UNIX systems on which it is built, is based on the key idiom that "everything is file." This is a powerful metaphor and model that dramatically simplifies writing programs to communicate with all sorts of devices. How can you use the write() system call to write data to a text file; to send data to a printer; to send keystrokes to an application; and, if you had, to tell your network-connected coffee pot to brew another pot of coffee.

The file metaphor works because Linux treats all devices, such as modems, CD-ROM drives, disc drives, keyboards, mice, as if they were files. Device drivers, which are part of the kernel, sit between a device and the user application to access it. A device driver translates an application's write() call into a form that the device can understand.

So, if an application uses the write() system call to write data to a text file on an ext3 file system, the ext3 driver writes the necessary bytes to a file on the disk, but if the application uses the write() system call to write same data to a printer, the printer driver transmits data out the parallel port (or across the network) in a manner that the printer can understand and interpret. This is one way how the Linux development environment informs, or defines, writing programs on a Linux system.

The catch? If the device you want to use doesn't have a driver, you can't use the write() to do anything with that device. You simply do not have a way to communicate with the device. This is how the Linux development environment constrains programming on a Linux system.

What, then, in addition to the file idiom already discussed, are the key features of Linux that characterize its development environment? In no particular order:

- The process model
- CPU and memory protection
- The security model

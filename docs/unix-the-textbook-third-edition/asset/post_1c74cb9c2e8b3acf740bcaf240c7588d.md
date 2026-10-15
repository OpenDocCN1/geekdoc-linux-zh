
as 14 letters in System V and 255 letters in Berkeley Software Distributions (BSD). Most contemporary UNIX systems comply with the BSD naming scheme. You can use the getconf command on your PC-BSD system to display the maximum size of a file name in number of characters, as follows:

```
$ getconf _XOPEN_NAME_MAX
255
$
```

If you get an error message, then you can use the getconf NAME_MAX command. Although you can use any characters for file names, we strongly recommend that non-printable characters, white spaces (spaces and tabs), and shell metacharacters (described in Chapter 2) not be used because they are difficult to deal with as part of a file name. You can give file names any of your own or application-defined extensions, but the extensions mean nothing to the UNIX system. For example, you can give an .exe extension to a document and a .doc extension to an executable program. Some applications require extensions, but others do not. For example, all C compilers require that C source program files have a .c extension, but not all Web browsers require an .html extension for files for Web pages. Even so, extensions should be used—it helps keep track of which files are for what purposes. Some commonly used extensions are given in Table 4.1.

## 4.3.2 Directory

A directory contains the names of other files and/or directories (the terms directory and subdirectory are used interchangeably). In some systems, terms such as folder, drawer, or cabinet are used for a directory. A directory file in any operating system consists of an array of directory entries, although the contents of a directory entry vary from one system to another. In UNIX, a directory entry has the structure shown in Figure 4.1.

The inode number is four bytes long and is an index value for an array on the disk. An element of this array, known as an index node, more commonly called an inode, contains the attributes of a file such as file size (in bytes). When you create a new file, the UNIX kernel allocates an inode to it. Thus, every unique file in UNIX has a unique inode (and

### TABLE 4.1 Commonly Used Extensions for Some Applications

| Extension | Contents of File |
|---|---|
| .bmp, .jpg, .jpeg, .gif | Graphics |
| .c | C Source code |
| .C, .cpp, .cc | C++ Source code |
| .java | Java source code |
| .class | Java class file |
| .html, .htm | File for a Web page |
| .o | Object code |
| .ps | Postscript code |
| .Z, .gz | Compressed |

inode number). The details of an inode and how the kernel uses it to access a file's contents on disk are discussed in Section 4.6.

### FIGURE 4.1 Structure of a directory entry.

| Inode number | File name |
|---|---|

## 4.3.3 Link File

A file of type link “points to” an existing file. The content of a link file is the pathname of the existing file. Thus, a link file allows you to access an existing file through another path in the file system structure and share it without duplicating its contents. The concept of a link in UNIX is fully discussed in Chapter 8. But, for now, a file of type link is created by the system when a symbolic link is created to an existing file. Symbolic links are a creation of BSD UNIX but are currently available on almost all versions of UNIX.

## 4.3.4 Special (Device) File

A special file, also known as a device node, is a means of accessing hardware devices, including the keyboard, disks, tape drive, graphic cards, network cards, and printers. Each hardware device is associated with at least one special file—and a command or an application accesses a special file to access the corresponding device. Special files are divided into two types: character special files and block special files. Character special files correspond to character-oriented devices, such as a keyboard, and block special files correspond to block-oriented devices, such as a disk. Special files are typically placed in the /dev directory (see Section 4.4 for more details).

Applications and commands read and write peripheral device files in the same way that they read or write an ordinary file. That capability is the main reason that input and output in UNIX is said to be device independent. Various special devices simulate physical devices and are, therefore, known as pseudodevices. These devices allow you to interact with a UNIX system without using the devices that are physically connected to it. These devices are becoming more and more important, because they allow use of a UNIX system via a network or modem, or with virtual terminals in a window system such as the X Window System (see Chapter 23).

## 4.3.5 Named Pipe (FIFO)

UNIX has several tools that enable processes to communicate with each other. These tools, which are the key to the ubiquitous client–server software paradigm, are called interprocess communication (IPC) mechanisms (commonly known as IPC primitives or IPC channels). These primitives are called pipes, named pipes (also called FIFOs), and sockets (systems that are strictly System V–compliant have a mechanism called transport layer interface (TLI)). These primitives are discussed in detail under “System Programming” in Chapters 18 through 21. Here, we briefly mention the purpose of each so that you can appreciate the need for each mechanism and understand the need for FIFOs.

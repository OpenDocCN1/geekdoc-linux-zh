| Directory | Function |
|---|---|
| / | Begins the file system structure, called the root |
| /home | Contains users' home directories |
| /bin | Holds all the standard commands and utility programs |
| /usr | Holds those files and commands used by the system; this directory breaks down into several subdirectories |
| /usr/bin | Holds user-oriented commands and utility programs |
| /usr/sbin | Holds system administration commands |
| /usr/lib | Holds libraries for programming languages |
| /usr/share/doc | Holds Linux documentation |
| /usr/share/man | Holds the online manual Man files |
| /var/spool | Holds spooled files, such as those generated for printing jobs and network transfers |
| /sbin | Holds system administration commands for booting the system |
| /var | Holds files that vary, such as mailbox files |
| /dev | Holds file interfaces for devices such as the terminals and printers |
| /etc | Holds system configuration files and any other system files |

TABLE 10-1 Standard System Directories in Linux

> NOTE The overall organization of the Linux file structure for system directories and other useful directories such as those used for the kernel are discussed in detail in Chapter 33.

# Listing, Displaying, and Printing Files: ls, cat, more, less, and lpr

One of the primary functions of an operating system is the management of files. You may need to perform certain basic output operations on your files, such as displaying them on your screen or printing them. The Linux system provides a set of commands that perform basic file-management operations, such as listing, displaying, and printing files, as well as copying, renaming, and erasing files. These commands are usually made up of abbreviated versions of words. For example, the ls command is a shortened form of "list" and lists the files in your directory. The lpr command is an abbreviated form of "line print" and will print a file. The cat, less, and more commands display the contents of a file on the screen. Table 10-2 lists these commands with their different options. When you log in to your Linux system, you may want a list of the files in your home directory. The ls command, which outputs a list of your file and directory names, is useful for this. The ls command has many possible options for displaying filenames according to specific features.
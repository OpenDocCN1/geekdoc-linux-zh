When you installed Linux, one of the first things you did was create a file system. In the process, you carved out a chunk of hard disk and formatted it so that Linux could use it. You also created a hierarchical (treelike) structure for storing files, to impose some order on the file system to help both you and the Linux system find needed files.

In this chapter, you’ll learn how to work with files and directories in a Linux system. You’ll understand how the file system is structured to separate system data from personal data and how to navigate through it. We’ll cover three ways to manipulate your files: using the command line, the Midnight Commander, and the graphical File Manager.

When you’re done, you’ll be creating, deleting, copying, renaming, listing, linking, and protecting your files like a pro. You’ll also learn the Nine Deadly Keystrokes—or how to wipe out the entire file system without really trying. (But don’t worry; this command can affect you only if you’re logged in as root.)

Log in as hermie and try the examples in this chapter as you read through it. You’ll find that the Linux file system is a lot like DOS, only more robust and flexible.

# What Is a Linux File?

We’ve created a structured file system and filled it with a whole bunch of files—without knowing what Linux files are. Here’s what files are in the Linux world and how they are named.

# Types of Files

In most operating systems, a file is simply a blob of data stored on disk with a unique name. A file could be a list of names and numbers, a cheesecake recipe, or an executable program. But under Linux, everything is a file. In addition to data and executable files, Linux treats directories and even the various components of your computer as files.

This means there are files that represent your keyboard, console, printer, CD-ROM, and even your system’s RAM. These special files are called devices, and they are found in the /dev directory (see Figure 5-1). (If you look in this directory later, you’ll see files such as /dev/fdo
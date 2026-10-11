![](bbox=[0.17, 0.11, 0.23, 0.16])

# NOTE

> The Tab-completion feature of the BASH shell can also be used to specify the path-name to files and executable programs as well as directories.

# ## Viewing Files and Directories

After a directory structure exists to organize files into an easy-to-use format, you can list directory contents to locate the file you need to execute, view, or edit. Before doing this, you should understand the various types of files and filenames that can be listed, as well as the different commands used to select filenames for viewing.

# ### File Types

Fundamental to viewing files and directories is a solid understanding of the various types of files present on most Linux systems. Several different types of files can exist on a Linux system; the most common include the following:

+   ◆ Text files
+   ◆ Binary data files
+   ◆ Executable program files
+   ◆ Directory files
+   ◆ Linked files
+   ◆ Special device files
+   ◆ Named pipes and sockets

Most files on a Linux system that contain configuration information are **text files**. Programs are also files that exist on the hard drive before they are executed in memory to become processes, and are usually associated with several supporting **binary data files** that store information such as common functions or graphics. In addition, directories themselves are just special files that serve as placeholders to organize other files. When you create a directory, a file is placed on the hard drive to represent that directory.

**Linked files** are files that have an association with one another; they can represent the same data or they can point to another file (also known as a shortcut file). **Special device files** are less common than the other file types that have been mentioned, yet they are important for systems administrators because they represent different devices on the system, such as hard disks and serial ports. These device files are used in conjunction with commands that manipulate devices on the system; special device files are typically found only in the *dev* directory and are discussed in later chapters of this book. As with special device files, **named pipe files** are uncommon and used primarily by administrators. Named pipes identify a channel that
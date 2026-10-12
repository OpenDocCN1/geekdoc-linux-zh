# Chapter 4: Navigating the Red Hat Linux File System

# In This Chapter

+   - Understanding the Red Hat Linux file system
+   - Navigating the file system with Linux commands
+   - Understanding file permissions
+   - Manipulating files and directories with Linux commands

To use files and directories well, you need to understand the concept of a hierarchical file system. Even if you use the GUI file managers to access files and folders (folders are another name for directories), you can benefit from a lay of the land of the file system.

In this chapter, I introduce you to the Linux file system. Then you learn to work with files and directories with several Linux commands.

# Understanding the Red Hat Linux File System

Like any other operating system, Red Hat Linux organizes information in files and directories. Directories, in turn, hold the files. A directory is a special file that can contain other files and directories. Because a directory can contain other directories, this method of organizing files gives rise to a hierarchical structure. This hierarchical organization of files is called the file system.

The Red Hat Linux file system gives you a unified view of all storage in your PC. The file system has a single root directory, indicated by a forward slash (/). Then there is a hierarchy of files and directories. Parts of the file system can reside in different physical media, such as hard disk, floppy disk, and CD-ROM. Figure 4-1 illustrates the concept of the Red Hat Linux file system (which is the same in any Linux system) and how it spans multiple physical devices.

If you're familiar with MS-DOS or Windows, you may find something missing in the Red Hat Linux file system: There are no drive letters in Red Hat Linux. All disk drives and DVD/CD-ROM drives are part of a single file system.
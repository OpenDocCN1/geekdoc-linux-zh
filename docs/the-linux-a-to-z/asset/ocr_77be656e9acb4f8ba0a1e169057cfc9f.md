# 1.2 The File Hierarchy

Having logged on to the system, the next task is to familiarize yourself with the basic file system layout. The Linux file system consists of files that fall into three basic classes:

+   - **Ordinary files.** These are just collections of bytes upon which the system imposes no particular structure. They are used for text documents (including program source code), data files for programs to use and even the binary executable program files themselves.
- **Directory files.** A directory is the mechanism that allows sets of files to be grouped together. Conceptually, the directory forms a container into which other files and directories can be placed, though, in fact, the directory itself actually contains only the names of the other files plus some simple information on how to find them on disk. Because a directory can itself contain the names of subdirectories, the file system forms a hierarchy.
- **Special files.** A number of different file types fall into this category and you will see them all as you progress through the book. But, in the main, the special files are associated with communicating between running processes and also allowing processes to communicate with the various hardware devices that are connected to the machine, such as terminals, CD-ROMs, modems, etc.

All these file types are arranged into a large tree structured hierarchy (see Figure 1.1). This tree has a single directory at the top, called the root directory (not to be confused with the root login name), which is given the symbolic name '/'. Inside the root directory are several other standard directories and files which are used for various purposes. The layout of these higher level directories and files is standard only by convention and not by necessity, though it would be most confusing once you knew the conventions to find a directory hierarchy that was not laid out in the standard way.

Figure 1.1 shows a root directory (/) that contains the subdirectories dev, bin and home. The directory home in turn contains the directories mike and lynne, and so on. At the lowest levels, the directories contain the ordinary files and special files (like a and b). Given these file relationships, you would say that 'home is the parent of mike and that a is a child of proj1'. It is quite possible for two or more files or directories to have the same name as long as they are contained in different parent directories. Obviously, therefore, there has to be some method for referring to a particular file unambiguously. This is done by specifying a pathname. A pathname is just a list of names separated by slash (/) characters. If this list of names also begins with a slash character then it is called an absolute pathname, which means that it works down from the root directory. For example, the absolute pathname for the directory proj1 is:

```
/home/lynne/proj1
```

and for the special file b it is:
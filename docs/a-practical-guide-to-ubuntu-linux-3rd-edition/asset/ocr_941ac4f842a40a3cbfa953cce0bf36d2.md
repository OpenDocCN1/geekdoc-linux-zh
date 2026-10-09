# ## Basic Utilities

One of the important advantages of Linux is that it comes with thousands of utilities that perform myriad functions. You will use utilities whenever you work with Linux, whether you use them directly by name from the command line or indirectly from a menu or icon. The following sections discuss some of the most basic and important utilities; these utilities are available from a CLI. Some of the more important utilities are also available from a GUI; others are available only from a GUI.

# Run these utilities from a command line

> **tip** This chapter describes command-line, or textual, utilities. You can experiment with these utilities from a terminal, a terminal emulator within a GUI (page 125), or a virtual console (page 149).

**Folder/directory** The term *directory* is used extensively in the next sections. A directory is a resource that can hold files. On other operating systems, including Windows and Macintosh, and frequently when speaking about a Linux GUI, a directory is referred to as a *folder*. That is a good analogy: A traditional manila folder holds files just as a directory does.

# In this chapter you work in your home directory

> **tip** When you log in on the system, you are working in your *home directory*. In this chapter that is the only directory you use. All the files you create in this chapter are in your home directory. Chapter 6 goes into more detail about directories.

# ## ls: Lists the Names of Files

Using the editor of your choice, create a small file named **practice**. (A tutorial on the vim editor appears on page 186.) After exiting from the editor, you can use the ls (list) utility to display a list of the names of the files in your home directory. In the first command in Figure 5-1, ls lists the name of the **practice** file. (You may also see files that the system or a program created automatically.) Subsequent commands in Figure 5-1 display the contents of the file and remove the file. These commands are described next.

```
$ ls
practice
$ cat practice
This is a small file that I created
with a text editor.
$ rm practice
$ ls
$ cat practice
cat: practice: No such file or directory
$
```

![](bbox=[0.21, 0.87, 0.95, 0.9])
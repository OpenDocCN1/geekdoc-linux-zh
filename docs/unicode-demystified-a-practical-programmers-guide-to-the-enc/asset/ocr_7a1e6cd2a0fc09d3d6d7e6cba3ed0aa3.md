# Basic Utilities

Press CONTROL-X to exit pico. You are given the option of saving the buffer to a file: Y saves the buffer and N discards. If you choose to keep the buffer, you can then enter or change the filename that the buffer is written to.

# Basic Utilities

One of the important advantages of GNU/Linux and other variants of UNIX is that they come with several hundred utilities that perform many functions. You will use utilities whenever you use GNU/Linux, whether you use them directly by name from the command line or indirectly by a menu or icon. The following sections discuss some of the most basic and important utilities that you need to know. They are available from a character-based interface. Some of the most important utilities are also available from a GUI, and some are available only a GUI.

The term directory is used extensively in the next sections. A directory is a resource that can hold files. On other operating systems, including MS Windows, a directory is referred to as a folder, which is a good analogy: A directory is a folder that can hold files. When you log in on the system, you are working in a directory that is called your home directory. In this chapter that is the only directory you use: All the files you create in this chapter are in your home directory.

# ls: Lists the Names of Files

Using the editor of your choice, create a small file named practice in your directory. After exiting the editor, you can use the ls (list) utility to display a list of the names of the files in the directory. The first command in Figure 2-13 shows listing the name of the practice. (You may also see files that were put by your system administrator or automatically created by a program you ran.) Subquent commands in Figure 2-13 display the contents of the file and remove the file. These commands are described next.

```
$ ls
practice
$ cat practice
This is a small file that I created
with a text editor.
$ rm practice
$ ls
$ cat practice
cat practice: No such file or directory
```

Figure 2-13 Using ls, cat, and rm on the practice file
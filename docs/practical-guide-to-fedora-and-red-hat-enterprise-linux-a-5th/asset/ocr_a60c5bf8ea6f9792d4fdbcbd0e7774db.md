(page 159) through a pipe (page 158) to od (see the od man page) to display CONTROL-U as octal 25 (O25):

```
`$ echo xxxx\xxCONTROL-V CONTROL-U | od -c
000000    x   x   x   x   x  025   \n
0000010`
```

The `\n` is the NEWLINE character that `echo` sends at the end of its output.

# # BASIC UTILITIES

One of the important advantages of Linux is that it comes with thousands of utilities that perform myriad functions. You will use utilities whenever you work with Linux, whether you use them directly by name from the command line or indirectly from a menu or icon. The following sections discuss some of the most basic and important utilities; these utilities are available from a character-based interface. Some of the more important utilities are also available from a GUI; others are available only from a GUI.

+   - **Folder** The term *directory* is used extensively in the next sections. A directory is a resource that can hold files. On other operating systems, including Windows and Macintosh, and frequently when speaking about a Linux GUI, a directory is referred to as a folder. That is a good analogy: A traditional manila folder holds files just as a directory does.

+   - **In this chapter you work in your home directory**

+   - **Tip** When you log in on the system, you are working in your *home directory*. In this chapter that is the only directory you use: All the files you create in this chapter are in your home directory. Chapter 6 goes into more detail about directories.

# ## ls: LISTS THE NAMES OF FILES

Using the editor of your choice, create a small file named practice. (A tutorial on the vim editor appears on page 174.) After exiting from the editor, you can use the ls (list) utility to display a list of the names of the files in your home directory. In the first command in Figure 5-1 (next page), ls lists the name of the *practice* file. (You may also see files the system or a program created automatically.) Subsequent commands in Figure 5-1 display the contents of the file and remove the file. These commands are described next.

# ## cat: DISPLAYS A TEXT FILE

The `cat` utility displays the contents of a text file. The name of the command is derived from *concatenate*, which means to join together, one after the other. (Figure 7-8 on page 234 shows how to use cat to string together the contents of three files.)
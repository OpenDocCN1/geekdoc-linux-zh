But you can use a symbolic link, as follows:

```
# ln -s /usr/local/games play
```

```
# ls -l play
lrwxrwxrwx 1 bball users 16 Jan 5 14:12 play -> /usr/local/games
```

Now, instead of typing a long command like

```
# cd /usr/local/games
```

you can use

```
# cd play
```

![](bbox=[0.22, 0.5, 0.3, 0.6])

> Symbolic links to other directories on other file systems, such as a DOS or Windows partition, can be handy. For example, having a directory called dos in your home directory that is linked to /mnt/dos/windows/desktop makes copying or moving files to and from Linux and Windows a lot easier. For example, if you want to have a linked directory named dos in your home directory and your DOS file system is mounted under the /mnt/dos directory, first make sure that the DOS file system is mounted, and then use the ln command to create a symbolic link, like so:
> 
> # ln -s /mnt/dos/windows/desktop dos
> 
> See Hour 22 for details about mounting other file systems.

So far, you've learned about using the command line. If you're familiar with more graphical interfaces for manipulating files, you'll like the next program, mc.

# Handling Files with the Midnight Commander Program

The mc program, called Midnight Commander, is a graphical interface for handling files (see Figure 5.1). It is a visual shell (you'll learn more about shells in the next hour, "Using the Shell"). To start mc, type the following at the command line:

```
# mc
```

This section does not cover all the details of the mc program. Here are the highlights of its features:

+   - Provides a visual interface to two directories at a time
+   - Enables directory browsing with mouse clicks
+   - Enables menu-driven file operations with dialog boxes, mouse, keyboard and function key support
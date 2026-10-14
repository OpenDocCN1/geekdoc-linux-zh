You can step through the man pages by pressing the spacebar or using the arrow keys to scroll forward and backward through the man page text (assuming your terminal emulation package supports the arrow key functions). To exit the man pages, just hit the Q key.

To see information about the bash shell, look at the man pages for it using the command:

```
$ man bash
```

This command allows you to step through the entire man pages for the bash shell. The information is extremely handy when working on the command line because you don't have to refer to books or Internet sites to look up specific formats for commands. The manual is always there for you in your session.

# Traversing Directories

The change directory command (cd) is what you use to move your shell session to another directory in the Ubuntu filesystem. The format of the cd command is pretty simple:

```
cd destination
```

The cd command may take a single parameter, destination, which specifies the directory name you want to go to. If you don't specify a destination on the cd command, it will take you to your home directory.

The destination parameter can be expressed by two methods:

+   ♦ An absolute filepath
+   ♦ A relative filepath

The following sections describe the differences between these two methods.

# Absolute Filepaths

You can reference a directory name within the Ubuntu virtual directory using an absolute filepath. The absolute filepath defines exactly where the directory is in the virtual directory structure, starting at the root of the virtual directory. Thus, to reference the X11 directory that's in the lib directory, which in turn is in the usr directory, you would use the absolute filepath:

```
/usr/lib/X11
```

With the absolute filepath there's no doubt as to where you want to go. To move to a specific location in the filesystem using the absolute filepath, just specify the full pathname in the cd command:

```
rich@testbox:~$cd /etc
rich@testbox:/etc$
```

The prompt shows that the new directory for the shell after the cd command is now /etc. You can move to any level within the entire Linux virtual directory structure using the absolute filepath:

```
rich@testbox:/etc$ cd /usr/lib/X11
rich@testbox:/usr/lib/X11$
```
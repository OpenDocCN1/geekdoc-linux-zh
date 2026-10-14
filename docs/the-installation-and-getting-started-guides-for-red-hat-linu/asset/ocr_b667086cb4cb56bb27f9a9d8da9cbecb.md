# The Getting Started Guide for Red Hat Linux 6.0

+   - **-f — force.** Overrides the interactive mode and moves without prompting. Unless you know what you're doing, this option doesn't play nice; be very careful about using it until you become more comfortable with your system.
+   - **-v — verbose.** Shows a list of the files being moved.

If you want to move a file out of your home directory and into another directory, you would type:

```
mv sneakers.txt tigger
```

or,

```
mv sneakers.txt /home/billy /home/billy/tigger
```

using absolute pathnames.

# Renaming Files

Actually, we've already covered half of renaming, because when you copy or move files, you can also rename. To copy the file sneakers.txt from our login directory to our tigger subdirectory, just type:

```
cp sneakers.txt tigger
```

To copy and rename that file from sneakers.txt to piglet.txt, type:

```
cp sneakers.txt tigger/piglet.txt
```

To move and rename the file, just substitute mv for cp in the above example. If you cd to tigger and use ls, you'll see the file piglet.txt. If you just want to rename the file and keep its location, just mv in your current directory:

```
mv sneakers.txt piglet.txt
```

# Deleting Files and Directories

We talked about creating files with the touch command and by using redirection in Chapter 2. And we created the directory tigger using mkdir.
# CHAPTER 5 First Steps with Linux

> TIP
One of the best reasons to learn how to use emacs is that you can use nearly all the same keystrokes to edit commands on the bash shell command line. Another reason is that like vi, emacs is universally available on every UNIX and Linux system, included Apple's Mac OS X.

# Working with Permissions

Under Red Hat Linux (UNIX), everything in the file system, including directories and devices, is a file. Every file on your system has an accounting set of permissions based on ownership. These permissions form the basis for security under Linux, and designate each file's read, write, and execute permission for you, members of your group, and all others on the system.

You can examine the default permissions for a file you create by using the uname command, or as a practical example, by using the touch command and then the ls command's long-format listing like this:

```
$ touch file
$ ls -l -1 file
-rw-rw-r--  1 bball bball  Jul 23 12:28 file
```

In this example, the touch command is used to quickly create a file. The ls command then reports on the file, displaying information (from left to right) in the first field of output (such as -rw-rw-r-- (previously))

+   - The first character of the field is the type of file created—Common indicators of the type of file are a leading letter in the output. A blank (in the preceding example, which is represented by a dash) designates a plain file, d designates a directory, c designates a character device (such as /dev/tty0), and b is used for a block device (such as /dev/hda).
- Permissions—Read, write, and execute permissions (for the owner, group, and all others on the system. (You learn more about these permissions later in this section).
- Number of links to the file—The number one designates that there is only one file, whereas any other number indicates that there might be one or more linked files. Links are created with the ln command. A hard-linked file is an exact copy of the file, but it might be located elsewhere on the system. Symbolic links of directories can also be created, but only the root operator can create a hard link of a.
- The owner—The account that created or owns the file; you can change this designation by using the touch command.
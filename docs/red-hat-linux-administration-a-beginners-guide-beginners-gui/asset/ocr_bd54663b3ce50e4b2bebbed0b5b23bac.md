# # Removing Directory: rmdir

The **rmdir** command offers no surprises for those familiar with the DOS version of the command; it simply removes an existing directory. The directory must be empty before you can remove it. The only command-line parameter available for this is **\-p**, which removes parent directories as well. For example, in a directory named /tmp/bigdir/subdir/mydir, if you want to get rid of all the directories from **bigdir** to **mydir**, you’d issue this command alone:

```
[root@tedford /tmp]# rmdir -p bigdir/subdir/mydir
```

To remove a directory called **mydir**, you’d type this:

```
[michael@workbox michael]$ rmdir mydir
```

> **NOTE** The **rmdir** command cannot be abbreviated to **rd** as it can under DOS.

# # Showing Present Working Directory: pwd

It is inevitable that you will sit down in front of an already logged-in workstation and not know where you are in the directory tree. To get this information, you need the **pwd** command. It has no parameters, and its only task is to print the current working directory. The DOS equivalent is typing **cd** alone on the command line; however, the BASH **cd** command takes you back to your home directory.

To get the current working directory, use this command:

```
[michael@workbox src]# pwd /usr/local/src
```

# # Tape Archive: tar

If you are familiar with the WinZip program, you are accustomed to the fact that the compression tool reduces file size but also consolidates files into compressed archives. Under Linux, this process is separated into two tools: **gzip** and **tar**.

The **tar** program combines multiple files into a single large file. It is separate from the compression tool, so it allows you to select which compression tool to use or whether you even want compression. Additionally, **tar** is able to read and write to devices in much the same way **dd** can, thus making **tar** a good tool for backing up to tape devices.
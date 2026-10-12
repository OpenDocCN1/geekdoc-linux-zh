TABLE 5.2 Continued

| Action | Command |
| --- | --- |
| Cursor right | Ctrl+f |
| Cursor up | Ctrl+p |
| Delete character | Ctrl+d |
| Delete line | Ctrl+k |
| Go to start of line | Ctrl+a |
| Go to end of line | Ctrl+e |
| Help | Ctrl+h |
| Quit | Ctrl+x, Ctrl+c |
| Save As | Ctrl+x, Ctrl+w |
| Save file | Ctrl+x, Ctrl+s |
| Search backward | Ctrl+r |
| Search forward | Ctrl+s |
| Start tutorial | Ctrl+h, t |
| Undo | Ctrl+x, u |

> > **TIP**
> > One of the best reasons to learn how to use emacs is that you can use nearly all the same keystrokes to edit commands on the bash shell command line. Another reason is that like vi, emacs is universally available on nearly every Unix and Linux system, including Apple's Mac OS X.

# Working with Permissions

Under Linux (and Unix), everything in the file system, including directories and devices, is a file. And every file on your system has an accompanying set of permissions based on ownership. These permissions form the basis for security under Linux, and designate each file's read, write, and execute permission for you, members of your group, and all others on the system.

You can examine the default permissions for a file you create by using the umask command, or as a practical example, by using the touch command and then the ls command's long-format listing like this:

```
$ touch file
$ ls -l file
-rw-rw-r-- 1 andrew andrew 0 Jul 23 12:28 file
```

In this example, the touch command is used to quickly create a file. The ls command then reports on the file, displaying information (from left to right) in the first field of output (such as -rw-rw-r- previously)
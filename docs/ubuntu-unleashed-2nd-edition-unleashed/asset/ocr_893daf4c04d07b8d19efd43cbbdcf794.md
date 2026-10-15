# Directory Permissions

Directories are also files under Linux. For example, again use the ls command to show permissions like this:

```
$ mkdir foo
$ ls -ld foo
drwxr-xr-x 2 andrew andrew 4096 2007-02-24 12:14 foo
```

In this example, the mkdir command is used to create a directory. The ls command and its -ld option is used to show the permissions and other information about the directory (not its contents). Here you can see that the directory has permission values of 775 (read+write+execute or 4+2+1, read+write+execute or 4+2+1, and read+execute or 4+1).

This shows that the owner and group members can read and write to the directory and, because of execute permission, also list the directory's contents. All other users can only list the directory contents. Note that directories require execute permission in order for anyone to be able to view their contents.

You should also notice that the ls command's output shows a leading d in the permissions field. This letter specifies that this file is a directory; normal files will have a blank field in place. Other files, such as those specifying a block or character device, will have a different letter.

For example, if you examine the device file for a Linux serial port, you will see

```
$ ls -l /dev/ttyS0
crw-rw---- 1 root root 4, 0 2007-02-24 11:53 /dev/ttyS0
```

Here, /dev/ttyS0 is a character device (such as a serial communications port and designated by a c) owned by root and available to anyone in the uucp group. The device has permissions of 660 (read+write, read+write, no permission).
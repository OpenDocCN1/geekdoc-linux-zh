```
% touch test.277
% ls -l test.277
-r--- 1 taylor 0 Oct 12 14:39 test.277
```

4. What if you want to have files created with the default permission being read-only for everyone, read-write for the group, but read-only for the owner? Again, work backward. The desired permission is r-x rwx r-x, so create the opposite value (-w----w-), translate it into binary (010 000 010), and then translate that into a three-digit value: 202 (010 = 2, 000 = 0, 010 = 2).

# Note

As a rule of thumb, it’s best to leave the execute permission enabled when building umask values so the system doesn’t err when creating directories.

umask is something set once and left alone or just left to its default value for your system, which is typically what you want anyway. If you’ve tried various experiments on your computer, remember to restore your umask back to a sensible value to avoid future problems (though each time you log in to the system, it’s reset).

In the next hour, you’ll learn how to use the mkdir command to create new directories, and you’ll see how the umask value affects default directory access permissions.

# Task 5.7: Identifying Owner and Group for Any File or Directory

One of the many items of information that the ls command displays when used with the -l flag is the owner of the file or directory. So far, all the files and directories in your home directory have been owned by you, with the probable exception of the .. directory, which is owned by whoever owns the directory above your home.

In other words, when you enter ls -l, you should see your account name as the owner for every file in the listing.

If you’re collaborating with another user, however, there might well be times when you’ll want to change the owner of a file or directory after you’ve created and modified it. The first step in accomplishing this is to identify the owner and group.

Identifying the owner is easy: ls lists that by default. But how do you identify the group of which the file or directory is a part?

+   1. With the addition of a new command flag, -g, the ls command can show the group membership of any file or directory. By itself, -g doesn’t alter the output of ls, but when used with the -l flag, it adds a column of information to the listing. Try it on your system. Here is an example:

Click here to view code image

```
% ls -lg /tmp
-rw-r--r 1 root root 0 Oct 12 14:52 sh145
drwxr-xr-x 2 shakes root 512 Oct 12 07:23 shakes/
-rw--- 1 meademd com435 0 Oct 12 14:46 snd.12
-rw--- 1 dessy stuprsac 1191 Oct 12 14:57 snd.15
-rw--- 1 steen utech 1 Oct 12 10:28 snd.17
```
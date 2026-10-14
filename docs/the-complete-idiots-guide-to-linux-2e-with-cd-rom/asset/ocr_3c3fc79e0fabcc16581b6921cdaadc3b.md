If portions of the path already exist, those portions are preserved and missing portions are added to the path.

# Check This Out: Beware the Powers of root!

If you are logged in as root this applies to you: root is a special administrative account that grants unrestricted access to the entire system. This is very valuable when you need to perform system administration type tasks, but it is not an account that you want to use for any other purpose. The root account can perform certain actions that are irreversible, such as erasing all files in the disk or some other catastrophic type of thing.

Until you know more about Linux and UNIX in general, I would recommend that you don’t use the root account unless it is absolutely necessary, as in the case of adding software or configuring some sort of device.

If you are not logged into your own account, create one right now! See Chapter 18, “Users, Groups, and Passwords,” for more information.

# Removing an Empty Directory: rmdir

To remove an empty directory, use the rmdir command. The rmdir command is “safe” because it won’t remove the directory unless the directory is empty. It looks like this:

```
[alberto@digital alberto]$ mkdir empty
[alberto@digital alberto]$ rmdir empty
```

# Removing Files and Directories at the Same Time: rm -R

Usually when you want to erase a directory, you also want to dispose of all files it contains. In UNIX and Linux, this task is accomplished using the rm command that you saw earlier.

To produce that effect, rm needs to recursively delete files that it finds before it can delete a directory. While this is the proper technique, beware: You can easily erase lots of things before you even realize what’s going on. Don’t forget, the shell operates very quickly. Take care when removing files; this is crucial when you are logged in a root, as you could destroy your entire file system with just one command.
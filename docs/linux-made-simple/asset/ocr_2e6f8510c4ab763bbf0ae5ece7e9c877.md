# Terminal:
User accounts

Whether you want to have one user or a hundred on your computer, it’s time to explain the basics of user accounts on Linux.

Linux is a multi-user operating system, even if you are the only person using your computer. The most basic of systems has two users: you and the superuser, also called root. Every file or directory is owned by a user and has settings, called permissions, that specify who can read or write to it. This safeguards your files from being overwritten by another user, or possibly even read by them if so set. It also safeguards system files because they are owned by root and can only be changed by root. This includes writing to system directories, so only the root user can install new software there. So how do you install software? See the ‘Becoming root’ box opposite for the answer.

One word of caution when using data on multiple computers, such as with an external hard disk. While you may see your username as a name, say johnny99, the computer sees and stores it as a number, a UID or user ID. During installation, your distro will have created a root user, who always has a UID of 0, and a normal user. Most distros start at 1000 for the first general user, but some start at 500. The point is, it’s that number stored on the disk as the owner of a file, so the same username may not own the file when you move the disk to another computer.

# Create a user

Every user has a home directory. This is usually /home/username but it can actually be anywhere – the user created

to run a web server will have a home directory somewhere like /var/www. In addition to users, Linux also has groups. A group is basically a collection of users. For example if you have a USB scanner on your computer, you often need to be a member of the scanner group to be able to use it. Now that we understand usernames, groups, UIDs and home directories, we can create a user:

```
sudo useradd -m -c "John Smith" -g users -G scanner,audio john
```

We use sudo here because only the root user can create users. The -m option creates a home directory at /home/john. -c specifies a comment to store for the user, which is usually the user’s full name. -g sets the primary group of the user, while -G adds secondary groups. Finally, we give the username. Not all of these options are necessary – if you omit -g, a default group will be used. Some distros use a single group called users for all non-system users, while others create a separate group for each user. The groupadd command works in a similar way, as do both of their counterparts – userdel and groupdel.

# Add a password

We have created a user but he cannot log in yet because we haven’t given him a password.

```
sudo passwd john
```

will ask you for the password twice. The passwd command

# Different filesystems

![](bbox=[0.13, 0.72, 0.37, 0.83])

Running the mount command on its own shows the options a filesystem was mounted with. Here you see the mask setting for a FAT formatted USB stick (fmask and dmask do the same as umask, but only for files and directories respectively).

One area that causes confusion is that of permissions of mount points. It makes no difference what permissions and ownership are set on a mount point before a filesystem is mounted there; it acquires the permissions of the root directory of the filesystem you mount there. How you change things for the top-level directory of a filesystem depends on its type. In the case of Linux filesystems, this is simple: mount it and then use chmod or chown to set it up as you want. These settings will then apply whenever, and wherever, you subsequently mount that filesystem.

Windows filesystems, such as FAT on USB sticks, are treated differently. FAT has no concept of file ownership and NTFS has a system which is incompatible with Linux permissions, so the filesystem driver imposes default permissions. These generally set all files and directories to be owned by the user who mounted the device, otherwise you couldn’t write to it. File permissions usually default to rwxr-xr-x (or 755 if you prefer) by the automounter.

If you are mounting a filesystem manually, use the uid option to set ownership and umask for default permissions, like this:

```
sudo mount /dev/sdb1 /mnt/removable -o uid=john,umask=022
```

The umask is subtracted from 777 to give the permissions – 755 in this case. A umask of 0 enables all permissions.
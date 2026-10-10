
## Example 4.12 Inode and Timestamp Information with stat

To get inode information for a specific (namely *expired*) subdirectory in his home directory, Don Quixote enters

```
$ stat expired<Enter>
File: "expired"
Size: 4096 Blocks: 8 Directory
Access: (0775/drwxrwxr-x) Uid: ( 501/ quixote) Gid: ( 607/ knights01)
Device: 306 Inode: 109096 Links: 5
Access: Wed Jul 12 18:13:21 2001
Modify: Mon Jul 10 13:22:17 2001
Change: Mon Jul 10 13:22:17 2001
```

In the stat results shown in Example 4.12, let’s look at the Access, Modify, and Change lines:

- **Access** means that the file has been read or written to and tells us the time and date when that last happened. When a file is read but no changes are made to it, the access time is changed but not the modification or change times.
- **Modify** indicates that the contents of the file or directory have been changed and indicates the time and date when that last happened.
- **Change** tells us that the inode information has been changed and indicates the time and date when that last happened.

At this point, as we mentioned previously in Example 4.5, Don Quixote deletes the *expired* and *misc* directories and their contents. Figure 4.4 illustrates what Don Quixote’s portion of the RFI directory now looks like.

## Formatting and Accessing Floppy Disks

Many users, especially new or ex-DOS and ex-Windows users, do not know that they can use floppy disks with Linux/UNIX. Although many of us work with UNIX-type systems on large networks and have abandoned sneaker netting to varying degrees, most if not all users still require it from time to time. In this section, we will create a Linux-like ext2 file system on one floppy and a DOS file system on another floppy.

![](img/cae5c706c216875d12d4b7d28144cc71_134_0.png)

Figure 4.4 Don Quixote’s portion of the RFI directory structure.

### Floppies with ext2 File Systems

You can create and manipulate files on floppies in as many ways as the half-dozen types of file systems that Linux supports. The ext2 file system procedure described in this section should be used on floppies moving from one Linux-like system to another.

We will start at the beginning and format a floppy disk. Insert the floppy disk into your floppy disk drive. The following procedure could be done as a root user or as an ordinary user. Let’s do it as an ordinary user. So, with the floppy disk in the floppy drive, type

```
$ fdformat /dev/fd0H1440<Enter>
```

You had to specify that the floppy disk was in device /dev/fd0; that is, in the first floppy disk drive. (If it had been in a second floppy drive, you would have had to specify /dev/fd1.) You enter the H1440 (with no space between this specification and the /dev/fd0 device name) to tell the system that /dev/fd0 contains a 3.5-inch high-density floppy disk with a capacity of 1.44MB. If your floppy disk is of another type, refer to the fdformat man page for the appropriate description.

As the system executes the fdformat command, it responds with

```
Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.
Formatting . . . (counts to 80) done
Verifying . . . (also counts to 80) done
```

Now that the floppy is formatted, the next step is to create a file system on it. Linux supports a half a dozen or so types of file systems that you can create on a floppy. In this first procedure, we will create an ext2 file system to be compatible with the ext2 file systems created on the hard disk during the Linux installation. Continuing as an ordinary user, type

```
$ /sbin/mkfs -t ext2 /dev/fd0<Enter>
```

Ordinary users should use /sbin/mkfs as the command because the directory /sbin is probably not in their $PATH. If you had performed this task as the root user, you would only have had to enter mkfs as the command because /sbin is already in root’s $PATH environment variable.

The -t option indicates that the user is about to tell the system what kind of file system to install on the floppy disk. The option is followed by the argument ext2, which is the default Linux file system type. After you enter the command, the system executes it and responds with

```
mke2fs 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label:
OS Type: Linux
Block size = 1024 (log=0)
Fragment size = 1024 (log=0)
184 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
1 block group
8192 blocks per group, 8192 fragments per group
184 inodes per group
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
```

Simply put, the system has told you that it has finished formatting the floppy disk and is now awaiting further instruction. (For an explanation of the output, which is beyond the scope of this book, refer to one of the sources of information mentioned in Chapter 15, “Linux Documentation and Support.”)

The next step is to mount the file system, which means that the system must be told to make the newly defined file system (the newly formatted floppy disk, in this case) part of its tree-like file hierarchy. Enter the next command as the root user, because ordinary users, when they try it, will be disappointed. All they will get is the mount : only root can do that error message. Here, then, is the command:

```
# mount -t ext2 /dev/fd0 /mnt/floppy<Enter>
```

> NOTE It is best and easiest to perform this task (mounting file systems) as a root or superuser. For security reasons, an ordinary user is not allowed to mount or umount a file system. An ordinary user can get around this restriction, however, by using mtools, which we will discuss in Chapter 5.

The mount command tells the system to make the ext2 file system, found on /dev/fd0, part of the total file system and to refer to the newly added file system as /mnt/floppy (that is, a subdirectory called /floppy in a subdirectory called /mnt, all part of the root directory). You could call it other names, but this name is the Linux convention. If you have entered everything correctly, the system will do as you command and respond with another root prompt.

To view what has occurred thus far, enter the following line:

```
# ls -la /mnt/floppy<Enter>
```

The system responds with

```
total 14

drwxr-xr-x 3 username username 1024 Apr 28 16:36 .

drwxr-xr-x 4 root root 1024 Jan 31 11:31 ..

drwxr-xr-x 2 root root 12288 Apr 28 16:36 lost+found
```

The system has already named the largest subdirectory on the floppy **lost+found**. You can change its name if you want. Also, notice that ownership of the single-dot special file has been given to username because it was as an ordinary user that we began the procedure. If we had done the whole procedure as the root user, then ownership of the single-dot file would have been root root.

You are now ready to use the floppy disk as part of your file system, using Linux commands.

When you are through using the floppy disk and wish to remove it, please remember that you cannot just “pop” the floppy disk out right away. First, you have to unmount the floppy disk’s file system (again, as the root user) from the total file system. To do that, type

```
# umount /mnt/floppy<Enter>
```

or

```
# umount /dev/fd0<Enter>
```

Note that the command is **umount**, not “unmount.” Again, you have to be a root user to umount a file system just as you have to be a root user to mount it in the first place. In addition, you cannot umount from the floppy diskette’s own file directories; you have to cd out of them. Otherwise, you will get a device busy error message.

Now, you can remove the floppy. When you want to use it again, you must re-enter the *mount* statement to get Linux to recognize it again. But you do not have to edit the /etc/fstab file, because those specifications remain.

### DOS File Systems

In the previous section, we formatted a floppy disk to be compatible with a Linux-like ext2 file system. To sneaker net between a Linux system and a DOS file system, however, you use commands that are similar but different than those discussed in the preceding section. We will start again with formatting a floppy disk.

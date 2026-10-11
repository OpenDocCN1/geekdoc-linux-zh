
## 8.

You have a directory `/home/user/bin` that contains the scripts you wrote. What file would you edit to make sure this directory is on your path whenever you log on?

- a. .inputrc
- b. .profile
- c. .bashrc
- d. .path

Answer a is incorrect; the .inputrc file configures the command-line editor. Answer b is correct; you can change your path at every login by defining it in your .profile file. Answer c is incorrect; the .bashrc is used by non-login shells. Answer d is incorrect; there is not a configuration file called .path.

## 9.

You are frequently deleting the wrong files. What could you do to prevent this?

- a. Alias rm to rm -i
- b. Change all your files to hidden files
- c. Use cp instead of rm
- d. Use mv instead of rm

Answer a is correct; by re-creating an alias so that the command rm is always called with the -i option, rm will ask you to verify each file before it is deleted. Answer b is incorrect; hidden files also can be deleted. Answer c is incorrect; this would make a copy of every file you want to delete. Answer d is incorrect; this would just change the location of the file you want to delete.

## 10.

You have been working on a new script trying out each line at the command line. You finally got the command to sort a file right but now you have forgotten exactly what you typed. What would you type to find this information?

- a. sort ?
- b. cat .bash_history
- c. history
- d. source history

Answer a is incorrect; the sort command takes a filename as an argument. Answer b is incorrect; this would display what was saved in .bash_history from your last login session. Answer c is correct; the history command will display all the commands you have recently typed. Answer d is incorrect; you source configuration files to load environment variables you have changed.

# Maintaining the Filesystem

## While You Read

- 1. You have just received a CD containing a new application you want to install; however, when you insert the CD in your computer, you cannot access it. Why is this?
- 2. Several of your users have come to you asking why they cannot save a file to a floppy disk. What is causing this and how can you allow your users to use the floppy?
- 3. When you look at the contents of the `/proc` directory you see several directories with names that are numbers. What are these?
- 4. You want to limit the amount of disk space each of your users can use. What should you do?
- 5. The marketing department has created a report covering a recent survey. Each of the marketing employees wants a copy in their home directories to review the data. What should you do?
- 6. One of your users comes to you and says she thinks she has lost a document that she created yesterday. Even though she does not remember what name she gave the document, how could you locate this file?
- 7. You want all your users' documents to be referenced in the locate database. How can you make this happen?
- 8. You install a new application to /usr/bin; however, it does not behave as you expect. What could be the problem?

### Chapter Prerequisite

By this time, you should know how to use the Linux documentation as well as other resources to help you find more information when needed. You also should know how the Linux filesystem is organized and the basis of managing files.

# CHAPTER 6

## Mounting Filesystems

To access files on your system or run applications, you need to make these files available. For the exam you will need to understand how this process takes place. In addition, you will need to know how to manipulate this process.

To place your filesystems into the Linux hierarchy, you use the `mount` command. The filesystems you mount can be on a device such as a disk partition, floppy disk, or CD-ROM. You also can mount virtual filesystems such as the `/proc` filesystem or filesystems created for other operating systems. In fact, you can even mount filesystems that reside on a computer different from the one you are presently using.

The syntax for the mount command is

```
mount [options] [device] mount-point
```

The options that you can use with the mount command are listed in Table 6.1.

**Table 6.1 Options That Can Be Used with the mount Command**

| Option | Action |
|---|---|
| -a | Mount all filesystems listed in /etc/fstab. |
| -f | Check to see whether filesystem is mountable, but do not actually mount it. |
| -n | Do not write mount information in /etc/mtab. |
| -o option | Modify the mount. See Table 6.2 for possible options. |
| -r | Mount as read-only. |
| -t fs-type | Designate the type of filesystem being mounted. |
| -v | Display mounting information. |
| -w | Mount as read-write; default action. |

**Table 6.2 Special Modifiers Used with mount -o**

| Option | Action |
|---|---|
| exec | Binaries can be executed. |
| noauto | Do not mount automatically. |
| nosuid | Do not process the suid or sgid bit. |
| nouser | Users can't mount the filesystem. |
| ro | Mount as read-only. |
| rw | Mount as read-write. |
| user | Allow users to mount the filesystem. |

If you call `mount` without any arguments, it will display all the file systems that are presently mounted, as in

```
/dev/hda1 on / type ext2 (rw)
none on /proc type proc (rw)
/dev/hda9 on /home type ext2 (rw)
/dev/hda7 on /tmp type ext2 (rw)
/dev/hda5 on /usr type ext2 (rw)
/dev/hda6 on /var type ext2 (rw)
/dev/fd00 on /mnt/floppy type vfat (rw)
/dev/cdrom on /mnt/cdrom type iso9660 (ro)
```

The information returned includes the device, mount point, type of file system, and any options such as read-only.

> **Key Concept**
> Use the `mount` command without any arguments to see what file systems are presently mounted. To add or remove a file system, use the `mount` and `umount` commands.

If you use the `mount` command to mount a file system that is defined in the `/etc/fstab` file, the `mount` command looks at any options that have been defined and applies them when mounting the file system. To override these options you can use the `-o` option with the `mount` command.

In addition, you can use the `-o` option to apply options when mounting a file system that is not defined in the `/etc/fstab` file. The `/etc/fstab` file is discussed later in this chapter.

To mount a device, such as your CD-ROM, you could type

```
mount /mnt/cdrom
```

You do not need to specify additional information such as making it read-only or the file system type. Instead, the `mount` command consults the `/etc/fstab` file to see whether this mount point is defined.

### The /etc/fstab File

The `/etc/fstab` file defines each file system that the `fsck` utility checks by default. This file is also used by the `mount` and `umount` commands. A sample `/etc/fstab` is

```
/dev/hda1 / ext2 defaults 1 1
/dev/hda9 /home ext2 defaults 1 2
/dev/hda7 /tmp ext2 defaults 1 2
/dev/hda5 /usr ext2 defaults 1 2
/dev/hda6 /var ext2 defaults 1 2
/dev/hda8 swap swap defaults 0 0
/dev/fd0 /mnt/floppy msdos noauto,user 0 0
/mnt/cdrom /mnt/cdrom iso9660 noauto,ro,user 0 0
none /proc proc defaults 0 0
```

The fields of each line are

- The physical location of the filesystem or block device.
- The mount point. This is the place in the directory structure where the root of the filesystem is located.
- The filesystem type.
- Options to use when mounting the filesystem. If you want to use multiple options, separate them with commas and no white space.
- A number that determines whether to back up the filesystem if the dump utility is used.
- A number that tells fsck in what order to check the filesystems.

Although a filesystem can be mounted that is not listed in the /etc/fstab file, the filesystem must be listed to be mounted by the mount -a command or for a user to be able to mount a filesystem.

If you want to mount a filesystem that is not defined in the /etc/fstab file, you have to provide all the same information that is listed in the /etc/fstab file. So, if you wanted to mount a floppy with the vfat filesystem rather than the msdos filesystem defined in the previous /etc/fstab file, you would type

```
mount -t vfat /dev/fd0 /mnt/floppy
```

If you want to mount this floppy at a location other than /mnt/floppy, first make sure that an empty directory has been defined on your directory tree to use as its mount point. It is conventional to mount removable filesystems such as floppy disks under the /mnt directory; however, you can mount it anywhere on the directory tree you want.

# The /proc Filesystem

Notice on the last line of the /etc/fstab file that the device is designated as none and the filesystem is /proc. This is a virtual filesystem that does not exist on a physical device but rather is a way to present information that is stored in memory. Each process is shown as a subdirectory of the /proc directory.

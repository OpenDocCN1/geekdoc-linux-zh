When you are writing scripts, a useful weapon to know about is find’s -print0 option. In combination with xargs -0, this option makes the find/xargs combination work correctly regardless of the whitespace contained within filenames. For example, the command

```
$ find /home -type f -size +1M -print0 | xargs -0 ls -l
```

prints a long ls listing of every file in /home over one megabyte in size.

Unfortunately, HP-UX supports find -print0 but not xargs -0, and AIX has neither option. However, you can install the GNU findutils package on either system to obtain current versions of both find and xargs. (Alternatively, you can use the -exec option to find instead of xargs, though it’s fussier and less efficient.)

# 6.2 FILESYSTEM MOUNTING AND UNMOUNTING

The filesystem is composed of smaller chunks—also called filesystems—each of which consists of one directory and its subdirectories and files. It’s normally apparent from context which type of “filesystem” is being discussed, but for clarity in the following discussion, we use the term “file tree” to refer to the overall layout and reserve the word “filesystem” for the chunks attached to the tree.

Most filesystems are disk partitions or disk-based logical volumes, but as we mentioned earlier, they can be anything that obeys the proper API: network file servers, kernel components, memory-based disk emulators, etc. Linux and Solaris even have a nifty “loopback” filesystem that lets you mount individual files as if they were distinct devices. It’s great for developing filesystem images without having to worry about repartitioning your disks.

In most situations, filesystems are attached to the tree with the mount command. mount maps a directory within the existing file tree, called the mount point, to the root of the newly attached filesystem. The previous contents of the mount point become inaccessible as long as another filesystem is mounted there. Mount points are usually empty directories, however.

For example,

```
$ sudo mount /dev/sda4 /users
```

installs the filesystem stored on the disk partition represented by /dev/sda4 under the path /users. You could then use ls /users to see that filesystem’s contents.

A list of the filesystems that are customarily mounted on a particular system is kept in the /etc/fstab, /etc/vfstab (Solaris), or /etc/filesystems (AIX) file.

3. We say “in most situations” because Solaris’s ZFS filesystem has adopted a rather different approach to mounting and unmounting, not to mention many other aspects of filesystem administration. Long-time readers may be expecting a snippy comment about gratuitous incompatibility at this point, but the ZFS scheme is a clear improvement and we look forward to the day that it’s adopted by other systems. In the meantime, we must of necessity keep our ZFS coverage somewhat ghettoized. See page 264 for more details.
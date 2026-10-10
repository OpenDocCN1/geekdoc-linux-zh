total 14

drwxr-xr-x 3 username username 1024 Apr 28 16:36 .

drwxr-xr-x 4 root root 1024 Jan 31 11:31 ..

drwxr-xr-x 2 root root 12288 Apr 28 16:36 lost+found

The system has already named the largest subdirectory on the floppy **lost+found**. You can change its name if you want. Also, notice that ownership of the single-dot special file has been given to username because it was as an ordinary user that we began the procedure. If we had done the whole procedure as the root user, then ownership of the single-dot file would have been root root.

You are now ready to use the floppy disk as part of your file system, using Linux commands.

When you are through using the floppy disk and wish to remove it, please remember that you cannot just “pop” the floppy disk out right away. First, you have to unmount the floppy disk’s file system (again, as the root user) from the total file system. To do that, type

```
# mount /mnt/floppy<Enter>
```

or

```
# umount /dev/fd0<Enter>
```

Note that the command is **umount**, not “unmount.” Again, you have to be a root user to umount a file system just as you have to be a root user to mount it in the first place. In addition, you cannot umount from the floppy diskette’s own file directories; you have to cd out of them. Otherwise, you will get a device busy error message.

Now, you can remove the floppy. When you want to use it again, you must re-enter the *mount* statement to get Linux to recognize it again. But you do not have to edit the /etc/fstab file, because those specifications remain.

# DOS File Systems

In the previous section, we formatted a floppy disk to be compatible with a Linux-like ext2 file system. To sneaker net between a Linux system and a DOS file system, however, you use commands that are similar but different than those discussed in the preceding section. We will start again with formatting a floppy disk.
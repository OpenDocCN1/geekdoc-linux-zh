+   1. Check your hardware and decide on a disk type and model.
2. Add the disk hardware, paying attention to characteristics such as EIDE master/slave status and SCSI termination and ID.
3. Partition the disk in a way that's suitable for your system.
4. Create filesystems on the new disk's partitions.
5. Mount the new disk's partitions.

If you want to transfer data, you can do so in between steps 4 and 5. The usual procedure is to select a directory to move to the new disk. For instance, you might move /opt to a new disk. To do so, follow these steps:

+   1. Follow steps 1 through 4 just above.
2. Mount the new partition at a temporary location. This can be an existing mount point, such as /mnt/floppy; or one you create specifically for this purpose. The remaining steps assume that you're using /mnt/floppy as a temporary mount point.
3. Change to the base of the directory you want to move, as in `cd /opt`.
4. Type the following command to copy all files to the new filesystem:

```
# tar clpf - . | (cd /mnt/floppy; tar xvfp -)
```

**Note** The `-l` parameter keeps tar from moving into filesystems mounted on the source directory. If you want to transfer two current filesystems onto one new one, you'll need to omit this parameter. It's included in step 4 because omitting it can sometimes cause problems. In particular, be careful *not* to copy the `/proc` filesystem, which is a pseudo-filesystem that contains system information. Copying it is wasteful and potentially dangerous. Another potential pitfall lies in copying a filesystem on which the destination filesystem is mounted, which results in an endless loop unless the `-l` tar parameter is specified. Both problems are most likely to occur if you attempt to move the root (/) filesystem.

+   5. Check, as best you can, that the new partition contains the files that it should.
6. Remove the files from their original location. For instance, type `rm -r /opt/*`.

**Warning** Step 6 is potentially very dangerous. If there's been an error in copying the files, removing the originals will result in data loss. You might want to skip this step for a while. If you do, you can mount the new partition over the contents of the original directory. You'll then access the new partition rather than the old directory. When you're satisfied that all is well, temporarily unmount the new partition and come back to perform step 6.

+   7. Unmount the new partition from its temporary location.
8. Mount the new partition at the (now empty) directory that held the original files.
9. Edit /etc/fstab to reflect the new filesystem mount point.

This procedure allows you to remove much of the load from one disk by spreading it across two. You may encounter complications, however. Specifically, if you want to move a directory that's normally in heavy use, such as `/usr`, you may have problems deleting the directory. In such cases, you may need to resort to an emergency boot disk to perform steps 6 and 9, skipping the intervening steps.

# ## Replacing a Disk

Fundamentally, you can treat a disk transplant much as you do a disk addition; it's just that you're
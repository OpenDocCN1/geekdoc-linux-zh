The first line repeats the device node and prints the partition's size 1, along with the block 2 and fragment sizes 3. You'll get filesystem geometry information 4, a relic of the days when disk geometry bore some relationship to the hardware. Finally, newfs(8) prints a list of super-block backups 5. The larger your filesystem, the more backup superblocks you get.

If you want to use soft updates journaling, add the -j flag. To use soft updates without journaling, add the -u flag. After you’ve created the filesystem, you can enable and disable soft updates journaling, and plain soft updates, with tune fs(8).

# UFS Labeling

Device nodes can change, but labels remain constant. Best practice is to label GPT partitions, but you can’t label MBR partitions. UFS filesystems on an MBR can use a UFS label with the -L flag.

```
# newfs -L var /dev/ada3s1d
```

The labels appear in /dev/ufs. Use them in /etc/fstab and other configuration files to avoid disk renaming mayhem. You can’t apply UFS labels to non-UFS filesystems.

If you’re using UFS on GPT partitions, choose either GPT or UFS labels. Thanks to wethering, you’ll see only one label at a time and probably confuse yourself.

# Block and Fragment Size

UFS’s efficiency is proportional to the number of blocks and fragments read or written. Generally, FreeBSD can read a 10-block file in half the time it needs to read a 20-block file. The FreeBSD developers chose the default block and fragment sizes to accommodate the widest variety of files.

If you have a special-purpose filesystem that overwhelmingly contains either large or small files, you might consider changing the
The output of the `mkfs` command varies depending on the file system you've selected. The file system creation process typically takes just a few seconds, although this varies depending on the size and speed of the disk, the file system in question, and other factors.

In reality, `mkfs` is just a front end to file system-specific tools, most of which use the name `mkfs.file system`, where `file system` is the file system name, such as `ext3` or `jfs`. The `mke2fs`, `mkext3fs`, `mkreiserfs`, and `mkdosfs` programs are additional names for creating `ext2fs`, `ext3fs`, ReiserFS, and FAT file systems, respectively.

Once you've created a file system, you should check it by mounting it, as described in Task 5.4. You can then verify its size using `df` and be sure that you can write files to the disk and read them back.

# ### Creating Swap Space

Swap space enables your computer to treat disk space as if it were RAM—slow RAM, but memory in which active data can reside when real RAM is insufficient. For it to do so, though, you must first prepare a disk file or partition to be used as swap space. You do this with the `mkswap` command:

```
```bash
# mkswap /dev/sda5
```
```

![](bbox=[0.15, 0.455, 0.25, 0.495])

> As with the `mkfs` command, `mkswap` is potentially extremely destructive. Review the command carefully to be sure you've specified the correct disk and partition.

Another option for swap space is to use an ordinary disk file. You can create a disk file of any size using `dd`:

```
```bash
# dd if=/dev/zero of=/swap bs=1048576 count=500
```
```

This example creates a file in the root directory, called `/swap`, that's 500MB in size (500 units of 1,048,576 bytes each). Of course, in practice you'd put the file wherever you have available disk space. In any event, you can then prepare it much as you'd prepare a swap partition:

```
```bash
# mkswap /swap
```
```

To verify that your swap space is properly configured, you can test it by first using `free` to examine the amount of available swap space, then using `swapon` to activate the swap space, and then using `free` again:

```
```bash
# free
```
```

| |total|used|free|shared|buffers|cached|
|---|---|---|---|---|---|---|
|Mem:|512052|505548|6504|0|63064|106176|
|~/+ buffers/cache:|336308|175744||| |||
|Swap:|1261560|276004|985556||||

```
```bash
# swapon /dev/sda5
```
```
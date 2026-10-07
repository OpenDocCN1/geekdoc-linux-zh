partitions they use.

When you're done editing the partition table, look it over with the `p` command; then verify that everything's okay with the `v` command. Chances are that `v` will report your disk has some number of unallocated sectors. This is normal and reflects sectors lost to the standard PC method of accessing the disk. You should write down the partition numbers and your intended uses for them, so that you don't forget these details. Once you're satisfied with your new partitioning scheme, type `w` to commit the changes to disk and exit.

**Tip** Linux's `fdisk` does *not* alter any on-disk structures until you enter the `w` command. If you create an unusable disk structure and want to start over again from scratch, you can type `q` to quit without saving the changes. When you start `fdisk` again, you'll see the same starting conditions you saw initially.

# ## Creating a Filesystem

Filesystems aren't completely blank slates. To function, they rely upon the presence of certain key components, even when they contain no actual files. These initial data structures include pointers to the root directory and whatever data structures the filesystem uses to allocate space, boot sector code, and perhaps some files or directories required by the OS or filesystem (such as the lost+found directory that appears on every ext2 filesystem). The process of writing these core data structures to disk is sometimes referred to as *formatting a disk*. This term is common in the Microsoft world, but it's ambiguous, because it can also refer to creating new magnetic marks the disk mechanism uses to locate individual sectors on the disk. To avoid ambiguity, it's common in the Linux world to refer to the process of writing sector marks as *low-level formatting*, and to laying out initial filesystem data structures as *high-level formatting* or *creating* (or *making*) *a filesystem*.

For floppy disks, the DOS and Windows `FORMAT` command performs both low-level and high-level formats, although it may skip the low-level format if that's already been done. In Linux, the `fdformat` program (described earlier in "Accessing Floppy Disks") performs a low-level format on floppy disks. Under any OS, special utilities are used to perform low-level formats on hard disks and high-capacity removable disks. These utilities are sometimes integrated into the BIOS, especially for SCSI disks. It's unlikely that you'll need to perform low-level formats on hard disks.

In Linux, each filesystem has its own utility to create a filesystem. These utilities are usually named `mkfs.fstype`, where `fstype` is a code for the filesystem; for instance, `mkfs.ext2` to create an ext2 or ext3 filesystem. Often these utilities go by other names, too, such as `mke2fs`. The `mkfs` utility is a front-end to all these specific filesystem-creation programs. Here is the syntax for this command:

```
`mkfs [-t fstype] [options] device [size]`
```

The options to this command are as follows:

+   - `--t fstype` Specify the filesystem type with this option. Then `mkfs` calls `mkfs.fstype`.

+   - `options` You can pass filesystem--specific options to the program that does the actual filesystem creation. Precisely what options are available varies from one filesystem to another; check the `mkfs.fstype` man page for details. Common options include the following:

+     - `--c` Checks the device for bad blocks.

158
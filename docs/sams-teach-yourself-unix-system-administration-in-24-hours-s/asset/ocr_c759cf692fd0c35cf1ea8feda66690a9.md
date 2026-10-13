The Unix approach is quite a bit more sophisticated, because you can hook new disks up wherever you'd like. If you are perverse, you could even connect your floppy drive as `/tmp`, or your CD-ROM drive as `/home`.

Disks are hooked into the system with `mount`, and the `mount` command checks the `/etc/fstab` file (or the equivalent) to see what should be automatically included at boot-time.

But we're getting ahead of ourselves, so let's start at the beginning with low-level disk formatting.

In this hour you learn about

+   - Formatting disks with `fdisk`
+   - Adding a filesystem with `mke2fs`
+   - Mounting the new disk
+   - Fine-tuning your `/etc/fstab` configuration file

# Formatting Disks with fdisk

It might surprise you, but the old MS-DOS command for formatting hard disks is in fact the same one used in modern Unix systems too: `fdisk`. Of course, what it does behind the scenes is a bit different!

> Actually, while they seem to be the same, the Unix version of `fdisk` has some subtle differences, so if you want to create a disk for a Unix or Linux system, use the `fdisk` included with that OS.

By this point in your Unix journey, it should be no surprise that inconsistencies are rife in the Unix user interface. Although most commands have single-character command flags, some have full-word command flags. The `fdisk` command is a member of a third category of interface: On many systems, type `fdisk` and you'll enter a simple `fdisk` shell in which you can type various commands to configure your disk; then the changes actually take place as you quit. On other versions of `fdisk`, you'll need to specify the device name on the command line.

> If you forget to write out your changes, any configuration you make in the `fdisk` program will be lost.
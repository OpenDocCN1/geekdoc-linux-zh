# # Review Questions

+   1. You want to use `/media/cdrom` to access your CD-ROM drive, so you insert a CD-ROM into the drive and type `mount /media/cdrom /dev/cdrom` as root. You receive the error message `\u001fmedia/cdrom is not a block device.` Why did this happen?
+   	A. You must first prepare the mount point by typing `mountpoint /media/cdrom`; only then will the `mount` command succeed.
+   	B. The command reverses the order of the CD-ROM device file and the mount point; it should be `mount /dev/cdrom /media/cdrom`.
+   	C. The `/dev/cdrom` filename isn’t valid; you must determine what device file is associated with your CD-ROM drive.
+   	D. The CD-ROM is defective or the CD-ROM drive is malfunctioning. Try another CD-ROM and, if necessary, replace the drive.

+   2. What is wrong with the following `/etc/fstab` file entry? (Select all that apply.)
+   	`/dev/hda8  nfs  default  0 0`
+   	A. The entry is missing a mount point specification.
+   	B. All `/etc/fstab` fields should be separated by commas.
+   	C. The `default` option may only be used with ext2 file systems.
+   	D. `/dev/hda8` is a disk partition, but `nfs` indicates a network filesystem.

+   3. You want to discover the sizes of several dot files in a directory. Which of the following commands might you use to do this?
+   	A. `ls -la`
+   	B. `ls -p`
+   	C. `ls -R`
+   	D. `ls -d`

+   4. You want to move a file from your hard disk to a USB pen drive. Which of the following is true?
+   	A. You’ll have to use the `--preserve` option to `mv` to keep ownership and permissions set correctly.
+   	B. The `mv` command will adjust filesystem pointers without physically rewriting data if the pen drive uses the same filesystem type as the hard disk partition.
+   	C. You must use the same filesystem type on both media to preserve ownership and permissions.
+   	D. The `mv` command will delete the file on the hard disk after copying it to the pen drive.
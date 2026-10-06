# Review Questions

+   1. Why you might type **touch filename**?
   A. To move *filename* to the current directory
   B. To ensure *filename*'s timestamp holds the current time
   C. To convert *filename* from DOS-style to Unix-style end-of-line characters
   D. To test the validity of *filename*'s disk structures
   E. To write cached data relating to *filename* to the disk

+   2. What parameter can you use with `ln` to create a soft link? (Select two.)
   A. -s
   B. --soft
   C. --slink
   D. --symbolic
   E. -s1

+   3. You want to discover the sizes of several dot files in a directory. Which of the following commands might you use to do this?
   A. `ls -la`
   B. `ls -p`
   C. `ls -R`
   D. `ls -d`
   E. `ls -F`

+   4. You want to move a file from your hard disk to a USB flash drive. Which of the following is true?
   A. You'll have to use the `--preserve` option to keep ownership and permissions set correctly.
   B. The `mv` command will adjust filesystem pointers without physically rewriting data if the flash drive uses the same filesystem type as the hard disk partition.
   C. You must use the same filesystem type on both media to preserve ownership and permissions.
   D. The `mv` command will delete the file on the hard disk after copying it to the flash drive.
   E. You must use the FAT filesystem on the USB flash drive; Linux-native filesystems won't work on removable disks.
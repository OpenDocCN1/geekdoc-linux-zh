
```sh
# find /export/home/sarah | cpio -o -O sarah.cpio
544 blocks

# find /etc -mtime -2
/etc/saf/zsmon/_pmpipe
/etc/saf/_sapipe
/etc/mnttab
/etc/utmpipe

# find /etc/ -mtime -2 | cpio -o -O etc.cpio
16 blocks
#
```

## Recovering the root or /usr File System

Occasionally, the root or /usr file system needs to be recovered. Assuming that the file system has been backed up and that the backup is available, you can use the following procedure:

- 1. Select an available partition or, if additional hardware is required, install the new disk in the system and then format and create an appropriately sized partition.
- 2. Create a file system by using the **newfs** command or another command (such as the **mkfs** command).
- 3. Mount the new file system on a temporary mount point. Change the directory to the temporary mount point.
- 4. Use the **ufsrestore** command to restore the root or /usr backup to the new file system.
- 5. Remove the restoresymtable file created by the **ufsrestore** command.
- 6. Unmount the new file system.
- 7. Use the **fsck** command to check the new file system. Modify `/etc/vfstab` to identify the new root or /usr partition.
- 8. If you're recovering the root file system, use the **installboot**(1M) command to create a boot block on the new file system.
- 9. Reboot the system.

## Practice Questions

### Question 1

Which of the following can be backed up by using the **ufsdump** command? (Select all that apply.)

- [ ] a. File systems on hard disks
- [ ] b. Files on hard disks
- [ ] c. File systems on CD-ROMs
- [ ] d. Directories on hard disks

Answers a, b, and d are correct. You can back up file systems, files, and directories on hard disks by using the **ufsdump** command. File systems on CD-ROMs are not UFS file systems and cannot be backed up by using the **ufsdump** command. Therefore, answer c is incorrect.

### Question 2

Enter the command that can be used to instruct the Volume Manager daemon to mount a floppy disk.

The correct answer is **volcheck**.

### Question 3

Which command-line argument is used to disable support for files larger than 2GB?

- a. **-o no2gfiles**
- b. **-o nobigfiles**
- c. **-o largefiles**
- d. **-o nolargefiles**

Answer d is correct. The **-o nolargefiles** command-line argument disables support for files larger than 2GB. **-o no2gfiles** and **-o nobigfiles** are not valid command-line arguments. Therefore, answers a and b are incorrect. **-o largefiles** would enable (not disable) large file support. Therefore, answer c is incorrect.

### Question 4

Which of the following file systems is typically used for user-accessible commands?

- a. `root`
- b. `/usr`
- c. `/var`
- d. `/home`

Answer b is correct. The /usr file system is typically used for system commands. The root file system is used for the kernel and device drivers. Therefore, answer a is incorrect. The /var file system is used for logging and spooling. Therefore, answer c is incorrect. The /home file system is used for user home directories. Therefore, answer d is incorrect.

### Question 5

Which of the following commands can be used to create a UFS file system?

- a. `newfs /dev/rdsk/c0d1s7`
- b. `mkfs -t UFS /dev/rdsk/c0d1s7`
- c. `newfs /dev/dsk/c0d1s7`
- d. `newfs /dev/dsk/c0t1d1s7`

Answer a is correct. The newfs /dev/rdsk/c0d1s7 command creates a UFS file system. The correct command-line argument to specify a UFS file system is -F. Therefore, answer b is incorrect. newfs /dev/dsk/c0d1s7 and newfs /dev/dsk/c0t1d1s7 use logical block device names, but the newfs command requires logical raw device names. Therefore, answers c and d are incorrect.

### Question 6

Which of the following commands use logical block device names? (Select all that apply.)

- ☐ a. `mount`
- ☐ b. `umount`
- ☐ c. `fsck`
- ☐ d. `newfs`

![](img/b957f979417d9f16274c2eb52c8f2c9f_241_0.png)

Answers a and b are correct. The **mount** and **umount** commands use logical block device names. **umount** can also use a mount point. **fsck** and **newfs** both use logical raw device names. Therefore, answers c and d are incorrect.

### Question 7

Which of the following types of file systems can be mounted by using the **mount** command? (Select all that apply.)

- ☐ a. UDF
- ☐ b. UFS
- ☐ c. TMPFS
- ☐ d. HSFS

Answers a, b, c, and d are correct. UDF, UFS, TMPFS, and HSFS file systems all can be mounted by using the **mount** command.

### Question 8

Which of the following **tar** commands can be used to back up the /etc directory?

- ○ a. `tar cvf /dev/rmt/0 /etc`
- ○ b. `tar cvf /etc /dev/rmt/0`
- ○ c. `tar -cvf /dev/rmt/0 /etc`
- ○ d. `tar -cvf /etc/ dev/rmt/0`

Answer a is correct. **tar cvf /dev/rmt/0 /etc** can be used to back up the /etc directory. The proper order of command-line arguments is function, followed by backup device, followed by the files to back up. Therefore, answer b is incorrect. No hyphen is required before c. Therefore, answers c and d are incorrect.

### Question 9

Which of the following functions can be performed by the **fsck** command? (Select all that apply.)

- ☐ a. Mounting file systems
- ☐ b. Repairing corrupted file systems
- ☐ c. Checking for file system damage
- ☐ d. Displaying the amount of space used by each user

Answers b and c are correct. The **fsck** command can repair corrupted file systems and check for file system damage. Mounting file systems is the function of the **mount** and **mountall** commands. Therefore, answer a is incorrect. Displaying the amount of space used by each user is the function of the **quot** command. Therefore, answer d is incorrect.

### Question 10

**Which of the following statements is true about the command `find / -mtime +7 -print | cpio -o -O 7days.cpio`?**

- a. All files and directories under the `/` directory that were modified seven or more days ago will be used to create the 7days.cpio archive.
- b. Only files under the `/` directory that were modified seven or more days ago will be used to create the 7days.cpio archive.
- c. The command will fail because the `find` command-line arguments are incorrect.
- d. All files and directories under the `/` directory that were modified seven or fewer days ago will be used to create the 7days.cpio archive.
- e. The command will fail because the `cpio` command-line arguments are incorrect.

Answer a is correct. All files and directories under the `/` directory that were modified seven or more days ago will be used to create the 7days.cpio archive. The specified **find** command will also list directories. Therefore, answer b is incorrect. Nothing is wrong with the **find** or **cpio** command-line arguments. Therefore, answers c and e are incorrect. The plus sign (+) preceding the number of days associated with the **-mtime** command-line argument means *or more*; a minus sign (-) would imply *or less*. Therefore, answer d is incorrect.

### Question 11

**Which of the following commands can be used to create a single archive of one or more directories and files? (Select all that apply.)**

- a. `compress`
- b. `tar`
- c. `gzip`
- d. `zip`

Answers b and d are correct. Both **tar** and **zip** can be used to create archives of multiple files and directories. The **zip** command typically reduces file size by using a data compression algorithm, whereas the **tar** command may or may not reduce storage requirements. The **compress** and **gzip** commands can compress only a single file at a time (no directories). Therefore, answers a and c are incorrect.

### Question 12

Which file contains a list of file systems to mount during system boot or when the **mountall** command is used?

- a. `/etc/vfstab`
- b. `/etc/default/fs`
- c. `/etc/mnttab`
- d. `/etc/autofs`

Answer a is correct. The /etc/vfstab file system contains a list of file systems to mount during system boot or when mountall is used. /etc/default/fs contains the default file system type. Therefore, answer b is incorrect. /etc/mnttab contains the list of currently mounted file systems. Therefore, answer c is incorrect. The /etc/autofs file does not exist. Therefore, answer d is incorrect.

### Question 13

Which of the following commands can be used to position a tape loaded in device `/dev/rmt/0n` to the third data set after the tape has been rewound? (Select all that apply.)

- a. `mt -f /dev/rmt/0n fsf 2`
- b. `mt fsf 2`
- c. `mt -f /dev/rmt/0n fsf 3`
- d. `mt fsf 3`
- e. `mt asf 3`

Answers a, b, and e are correct. The **mt -f /dev/rmt/0n fsf 2**, **mt fsf 2**, and **mt asf 3** commands can be used to position a tape loaded in device /dev/rmt/0n to the third data set after the tape has been rewound. The **mt -f /dev/rmt/0n fsf 3** and **mt fsf 3** commands would position the tape to the beginning of the fourth data set. Therefore, answers c and d are incorrect.

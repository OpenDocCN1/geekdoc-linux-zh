
run cfgmgr -l iscsi0. The cfgmgr command prints no confirmation messages, but we can see that the new device has appeared by looking in the /dev directory (on our example system, the new disk is /dev/hdisk2) or by running smitty devices, navigating to the Fixed Disk category, and listing the entries. The latter option is perhaps safer since smitty explicitly shows that hdisk2 is an iSCSI volume.

To disconnect an iSCSI device, you must not only edit the configuration file and reload the configuration with cfgmgr but you must also delete the disk from smitty’s Fixed Disk list.

## 8.12 EXERCISES

E8.1 Describe any special considerations that an administrator should take into account when designing a storage architecture for each of the following applications.

- a) A server that will host the home directories of about 200 users
- b) A swap area for a site’s primary DNS server
- c) Storage for the mail queue at a large spam house
- d) A large InnoDB (MySQL) database

E8.2 Logical volume managers are powerful but can be confusing if not well understood. Practice adding, removing, and resizing disks in a volume group. Show how you would remove a device from one volume group and add it to another. What would you do if you wanted to move a logical volume from one volume group to another?

E8.3 Using printed or Internet resources, identify the best-performing SCSI and SATA drives. Do the benchmarks used to evaluate these drives reflect the way that a busy server would use its boot disk? What cost premium would you pay for SCSI, and how much performance improvement (if any) would you get for the money?

E8.4 Add a disk to your system and set up a partition or logical volume on the new disk as a backup root partition. Make sure you can boot from the backup root and that the system runs normally when so booted. Keep a journal of all the steps required to complete this task. You may find the script command helpful. (Requires root access.)

E8.5 What is a superblock and what is it used for? Look up the definition of the ext4 superblock structure in the kernel header files and discuss what each of the fields in the structure represents.

E8.6 Use mdadm and its -f option to simulate a failed disk in a Linux RAID array. Remove the disk from the array and add it back. How does /proc/mdstat look at each step?

★★ E8.7 What fields are stored in an inode on an ext4 filesystem? List the contents of the inode that represents the /etc/motd file. Where is this file's filename stored? (Tools such as hexdump and ls -i might help.)

★★ E8.8 Examine the contents of a directory file with a program such as od or hexdump. Each variable-length record represents a file in that directory. Look up the on-disk structure of a directory and explain each field, using an example from a real directory file. Next, look at the lost+found directory on a filesystem that uses them. Why are there so many names there when the lost+found directory is empty?

★★★★★ E8.9 Write a program that traverses the filesystem and prints the contents of the /etc/motd and /etc/magic files. But don't open the files directly; open the raw device file for the root partition and use the seek and read system calls to decode the filesystem and find the appropriate data blocks. /etc/motd is usually short and will probably contain only direct blocks. /etc/magic should require you to decode indirect blocks. (If it doesn't, pick a larger text file.)

Hint: when reading the system header files, be sure you have found the filesystem's on-disk inode structure, not the in-core inode structure. (Requires root access.)

## 9 Periodic Processes

![](img/14d78e3cecac4581d37024baf1e94cca_331_0.png)

Scripting and automation are the keys to consistency and reliability. For example, an adduser program can add new users faster than you can, with a smaller chance of making mistakes. Almost any task can be encoded in a Perl or Python script.

It’s often useful to have a script or command executed without any human intervention. For example, you might want to have a script verify (say, every half-hour) that your network routers and switches are working correctly, and have the script send you email when problems are discovered.¹

### 9.1 CRON: SCHEDULE COMMANDS

The cron daemon is the standard tool for running commands on a predetermined schedule. It starts when the system boots and runs as long as the system is up.

cron reads configuration files that contain lists of command lines and the times at which they are to be invoked. The command lines are executed by sh, so almost anything you can do by hand from the shell can also be done with cron.²

1. Many sites go further than this and send a text message to an administrator’s phone as soon as a problem is detected. See Chapter 21, Network Management and Debugging, for more details.

2. You can configure cron to use other shells as well.

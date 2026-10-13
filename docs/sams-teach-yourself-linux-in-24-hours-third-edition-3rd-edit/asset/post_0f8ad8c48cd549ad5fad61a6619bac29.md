
## Managing Disk Space

As you work with Linux, create new files, and install new applications, you may start to run short on hard drive space. Every once in a while, you need to check and see how much free space is left. If room is becoming scarce, you may need to free up some space or maybe even start limiting the space you allocate to users.

As the Linux system administrator, your job is to make sure there is enough free space on the hard drive and in the filesystem to store files and add new applications. Because the filesystem is divided into separate partitions (or devices), you will need to know the names of each of these partitions. The mount command tells you which filesystems are available. An example of the mount command is shown in Listing 14.1.

### LISTING 14.1 The Output of the mount Command

```
[root@localhost /root]# mount
/dev/hda1 on / type ext2 (rw)
/proc on /proc type proc (rw)
/dev/hda3 on /home type ext2 (rw)
none on /dev/pts type devpts (rw,mode=0622)
```

You'll find quite a bit of information in the output of the mount command. For each mounted filesystem, the device name appears followed by the mount point, the filesystem type, and the access privileges. In Listing 14.1, the first filesystem (where the root partition is mounted) is located at /dev/hda1, it is a Linux Extended Filesystem (ext2), and has read and write privileges. To maintain this system, close attention needs to be given to /dev/hda3, because this is where each user's home directory is stored, and to /dev/hda1, because that is where the rest of the filesystem is stored.

Once you know which filesystem you need to watch, you can use the df command to find out the size of each partition and the du command to see how much room individual files and directories take up within the filesystem. Once you learn how much room is being used, you can then take corrective measures to eliminate wasted space.

### The Syntax for the df Command

The df command lists the amount of available (or free) disk space for each filesystem mounted on the system. The df command displays the name of each mounted filesystem. It displays the size of the partition, the amount of used and free space for each filesystem, the percentage of space used, and the mount point. Here's the syntax for the df command:

```
df [options] [filename]
```

When the df command is used by itself, it displays information for each mounted filesystem. You can use the df command with a filename to list the information for a single file, a device (such as a partition on the hard drive), a mount point, or a specific directory within the filesystem. Free space can be calculated for separate filesystems in these different ways:

- List the disk space information for a specific device. In Listing 14.1, to see the information for the device where the root filesystem is mounted, type `df /dev/hda1` and press Enter.
- List the disk space information for a specific mount point. Using Listing 14.1 again, to view information for the /home mount point (which is stored in /dev/hda3), type `df /home` and press Enter.

Several command options can be used with df to change how used and available space are displayed:

- To display the total free and used space in kilobytes, type `df -k` and press Enter.
- To display the total free and used space in megabytes, type `df -m` and press Enter.

### The Syntax for the du Command

The du command displays the amount of space a directory (and any subdirectories contained within the directory) occupies within the filesystem. By default, the du command lists the directories contained within the current working directory. Here's the syntax for the du command:

```
du [options] [filename]
```

When you want to display the space used by a particular file or directory, specify a filename after the du command. For example, to see the amount of space used by each directory within the /home directory and the total space used by the /home directory, type `du /home` and press Enter.

Use command options with the du command to change how the used space is displayed:

- To display the total used space in kilobytes, type `du -k` and press Enter.
- To display the total used space in megabytes, type `du -m` and press Enter.

## Task: Monitoring Used Disk Space

You have several tools at your disposal to help you monitor how quickly your hard drive is filling up. These tools should be used on a regular basis to keep track of disk space usage and to help you decide when it is time to make room for more files. Here are a few guidelines for monitoring disk space:

1. Display the free disk space on each of the mounted filesystems. Type df and press Enter. An example of a system with two mounted partitions is shown in Listing 14.2.

### LISTING 14.2 The Output of the df Command

| Filesystem | Size | Used | Avail | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/hda1 | 1961M | 1376M | 485M | 74% | / |
| /dev/hda3 | 988M | 4M | 984M | 0% | /home |

2. Determine which filesystem is getting too full. A filesystem should contain between 5 and 30 percent free space. In Listing 14.2, the filesystem on /dev/hda1 only has 26 percent free space; it is time to create some extra space. The filesystem on /dev/hda3 is only 0 percent full (our users haven’t been very busy).

3. View the amount of space being used by a particular directory. This can help you track down oversized directories. Type du filename and press Enter.

![](img/782ecfdc0b083a767896cc983e10427f_239_0.png)

> Several directories tend to fill up fast. One is the /home directory, where system users store their files. The other is the /usr directory, where programs that are available to all users are stored. To see the disk usage for a particular user, type du /home/username and press Enter.

4. List all the directories on the system according to size. Type du / | sort -rn and press Enter. If the listing is too long, view the output in the less pager (type du / | sort -rn | less and press Enter). Figure 14.1 shows an example of the directory size listing displayed in the less pager.

5. Take the first step needed to increase free space on your system. Determine those places where there is not enough room and identify those files that could be deleted, archived, or compressed.

6. Create a regular schedule on which you check for free and used disk space. If the system users are quite active, you may want to look at their disk usage on a weekly basis.

### FIGURE 14.1

The largest directories are displayed at the top of the list.

![](img/782ecfdc0b083a767896cc983e10427f_240_0.png)

Directory size

Directory name

## Creating Additional Free Disk Space

When you find the filesystem filling up and you think you'll need more hard drive space, you need to take some sort of action to increase the space available for storing files and installing new applications. One solution is to add a second (or third) hard drive to the system. Here are some other ideas to help you keep as much free hard disk space on hand as possible:

- **Compress files.** There may be files in your home directory (or the home directories of other system users) that are used infrequently. Compress these files (using a utility such as gzip, covered in Hour 10, "Backing Up and Restoring the Filesystem") when they aren't needed. If you need to work with the file, it only takes a second to uncompress the file.
- **Delete files.** Delete files that you no longer need.
- **Archive files.** Archive files you do not use on a regular basis on a removable storage medium, such as a floppy or Zip disk.
- **Clean out any temporary directories.** Clean out directories such as the `/tmp` directory and reduce the size of system log files (these are found in the `/var/log` directory). Also, delete backup files that are automatically created by any programs you use.

You'll learn how to reduce the size of system log files in Hour 17, "Automating System Administration Tasks."

- Move files and delete directories. Linux sees directories as empty files. When a directory has a considerable amount of activity, such as when files are moved around, the directory size might not shrink when the directory is empty. To get around this, move all the files out of the directory and then delete the directory.
- Remove programs you don't use. When you installed Linux, quite a number of applications were installed along with the operating system. If you find that you don't use some of these applications, get rid of them. Hour 15, "Installing Software," tells you how to uninstall applications.
- Limit the amount of space. Limit how much space users can use to store files on the hard drive.

## Locating Unused Files on the System

One way to regain valuable hard drive space is to delete or back up files that have not been used in the recent past. Here's how to use the find command to list those files that are good candidates for the archives (or the trashcan):

- 1. Look for files in the entire filesystem that have not been accessed in the last 180 days. Type find / -atime +180 -print and press Enter. This locates all the files on the system not accessed in the last six months and displays the list on the screen. Some sample output is shown in Figure 14.2.

FIGURE 14.2
Use the find command to locate files that have not been used recently.

![](img/782ecfdc0b083a767896cc983e10427f_241_0.png)

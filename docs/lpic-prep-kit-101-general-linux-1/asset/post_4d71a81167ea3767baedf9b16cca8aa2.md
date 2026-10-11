
Answer a is incorrect; the starting cylinder must be the next one after the ending cylinder of the prior partition. Answer b is incorrect; fdisk takes only the name of the partition to divide as an argument. Answer c is correct; you must enter the starting cylinder, which has to be the next one after the ending cylinder of the last partition. You can then enter either the ending cylinder or the desired partition size, such as +80M, to create an 80MB partition. Answer d is incorrect; you must first specify the starting cylinder before the size of the partition.

3. You have three partitions on your hard disk and 2GB of free space. You need to install an application that needs two partitions, a 50MB and a 300MB partition. What should you do?
- a. Create two new partitions in the free space.
- b. Create a new primary partition of 350MB and then use mks to divide it.
- c. Create a new extended partition of 2GB in size and then create two logical drives, one 50MB and one 350MB in size.
- d. Back up one of your partitions, delete it, and then re-create it, making it 350MB bigger.

Answer a is incorrect; you can have only a total of four partitions. Answer b is incorrect; the mks command is used to create a filesystem on the new partition. Answer c is correct; because you can have only a total of four partitions, you must create an extended partition that can be divided into logical drives. Answer d is incorrect; although you could do this, it would not create the separate partitions you need.

4. After creating your swap partition, what do you need to do to make it available to use for swapping by the operating system?
- a. Format the partition with the mkfs command.
- b. Change the type of partition to type 82 using the fdisk command.
- c. Format the partition with the mkfs.swap command.
- d. Pass the name of the partition to the kernel at boot.

Answer a is incorrect; the swap partition does not need to be formatted. Answer b is correct; the swap partition needs to be designated as such by changing its type. Answer c is incorrect; there is no mkfs.swap command. Answer d is incorrect; you must change the type of a partition to make it a swap partition, not designate it as such on boot.

5. Which of the following pieces of information is not necessary to pass to the mkfs command?
- a. Filesystem type
- b. Size of partition in bytes
- c. Partition name
- d. Size of partition in blocks

Answer a is incorrect; you must tell mkfs the type of the filesystem to apply to the partition. Answer b is correct; the mkfs command does not need to know the number of bytes on the partition. Answer c is incorrect; you must tell mkfs which partition to format. Answer d is incorrect; you must tell mkfs how many blocks are present on the partition you are formatting.

6. The inode structure contains all of the following, except
- a. Filename
- b. Access permissions
- c. The file's owner
- d. Date and time the file was last accessed

Answer a is correct; the filename is stored in the directory, not the inode structure. Answer b is incorrect; the permission block is stored in the inode. Answer c is incorrect; both the owner and group names are stored in the inode. Answer d is incorrect; the times the file was last accessed and last modified are stored in the inode.

7. You want to run fsck on your root partition. Which of the following will not enable you to do this?
- a. Boot with a floppy and then run fsck on root.
- b. Start in single-user mode and then run fsck.
- c. Use fsck with the -f option to force the check.
- d. Configure fsck to run at boot.

Answer a is incorrect; if you boot from a floppy, you will be able to run fsck. Answer b is incorrect; booting into read-only, single-user mode will enable you to run fsck on root. Answer c is correct; there is no -f option to force fsck to run on a mounted filesystem. Answer d is incorrect; the most common time to run fsck on root is during boot.

8. You need to prepare a report for your supervisor with the total space used by each user. What command would help you prepare this report?
- a. du
- b. df
- c. ls -1
- d. wc

Answer a is correct; the du command displays the amount of disk space being used. Answer b is incorrect; the df command shows the amount of space used on an entire partition. Answer c is incorrect; this displays a list of all the files and their attributes. Answer d is incorrect; the wc command counts the words, characters, and lines in a file.

9. You need to prepare a report that will be the basis of planning for needed hard disk space expansion. What command could you use to help prepare it?
- a. du
- b. df
- c. ls -l
- d. wc

Answer a is incorrect; the du command displays the amount of disk space being used. Answer b is correct; the df command shows the amount of space used on each partition. Answer c is incorrect; this displays a list of all the files and their attributes. Answer d is incorrect; the wc command counts the words, characters, and lines in a file.

10. The partition containing users’ home directories is full. Which of the following solutions would not work?
- a. Create a new partition and move some users’ home directories to the new partition.
- b. Back up the data, delete and re-create the partition with a bigger size, and then restore the data.
- c. Delete or move unused files.
- d. Instruct users to save files in another partition.

Answer a is incorrect; by creating a new partition and moving some users’ home directories you will solve your space problem. Answer b is incorrect; this is the only method available to enlarge a partition. Answer c is incorrect; this would be a good stopgap measure, but your space problem will likely recur. Answer d is correct; by instructing users to save files to a different partition, your organization scheme becomes chaotic, making files harder to find.

### CHAPTER PREREQUISITE

You should be comfortable with typing on the command line, which is covered in Chapter 5, “GNU and UNIX Commands.” You should have a computer running Linux and have a clear understanding of the Linux filesystem as discussed in Chapter 3, “Linux Filesystem.” In addition, you should have read and understood Chapter 1, “Finding and Creating Documentation.”

![](img/8dd1e68596303df43cb8ccf3197e8e53_90_0.png)

### File Management

### WHILE YOU READ

1. How can you get a list of all the directories in your home directory sorted by time with the newest listed at the top?
2. What command would you use to combine the contents of three files?
3. How can you monitor system messages as they are written to the log file?
4. How do you change the access time on a file to the present time?
5. What command would you use to copy a group of files including its directory hierarchy from one location to another?
6. After editing several files in different directories you don’t remember where you are in the directory hierarchy. How can you discover where you are? How can you return to your home directory?
7. One of your users has a directory with over 300 files and cannot find the letter he wrote about the new medical plan. What would you tell him to do?
8. You have almost filled your disk quota but do not want to delete any files. What should you do?

### Basic File Management Commands

This chapter discusses the basic commands used to manage your files and directories. These commands are the foundation necessary for you to perform the day-to-day tasks associated with the job of system administration. Table 4.1 lists these commands along with a short description of each command's purpose.

| Command | Purpose |
| :--- | :--- |
| cd | Sets location in filesystem |
| ls | Displays contents of directory |
| file | Determines file's type |
| cat | Displays file's contents |
| more | Displays file's contents one screen at a time |
| less | Displays file's contents one screen at a time |
| wc | Shows character, word, and line counts |
| head | Displays first few lines of a file |
| tail | Displays last few lines of a file |
| touch | Changes file's timestamp; create an empty file |
| cp | Copies a file |
| dd | Copies a file from one device to another |
| mv | Changes a file's name or location in the filesystem |
| rm | Deletes a file |
| mkdir | Creates a directory |
| rmdir | Deletes a directory |

Many commands are used in performing file management, and you will need to be familiar with them for the exam. Rather than being asked what a command does, you will be asked about its functionality, or you will be given an example containing a command and have to predict the results of running that command. You also might see these commands used to solve a scenario question, so you need to be sure you understand each one.

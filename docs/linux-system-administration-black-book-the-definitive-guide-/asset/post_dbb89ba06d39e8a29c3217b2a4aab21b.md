
In this example, rwxr-xr--, consider each of the sets separately. The first set, rwx, is 4 + 2 + 1, or 7. The second set is 4 + 0 + 1, or 5. The third is 4 + 0 + 0, or 4. So the numeric permissions break down into 754.

### The Mask Vs. The Umask

The *mask* of a file system item is the same as its permission. The two terms are equivalent. Another useful item is the *umask*. This term refers to the bits that are not turned on in the mask or permission sets.

The umask is an incredibly useful tool for a system administrator. Many users do not understand permissions, and so never alter them when creating files and directories within their home directory. When users do this with weak default permissions, the act can cause security problems. Therefore, changing the default creation mask by setting the default umask to a stronger setting can save many headaches.

The umask for the rwxr-xr-- is ---w--wx. This format is unwieldy because it gets hard to keep track of dashes, so the umask is more often discussed in numeric terms. In fact, the format is not entirely correct. Technically it is, but due to security reasons you cannot make an item executable by default. Therefore, there will never be an odd number in a umask setting. So, instead, the umask for the example is ---w--w_, or 022.

### SUID And SGID

The terms SUID (set user ID) and SGID (set group ID) are tossed around a lot in Linux manuals without ever really discussing what they are used for. These terms are used when an executable must be able to run "as" a particular user or group member, rather than just a process belonging to that user or group. When you hear or read something telling you to "run the program as root," this is what the speaker is referring to.

### The Sticky Bit

Another odd phrase you might come across is "turn on the sticky bit." This permission bit is an extra piece of protection for some directories. Its primary use is for directories or hierarchies where everyone needs to have access to the contents, but no one should be able to touch anyone else's files. (Some examples where this is useful are the /tmp or /var/spool/mail directories.) If the sticky bit is used, then no user can delete, move, or rename a file unless he or she is the file's owner in the file listing; he or she is the directory's owner; or he or she is the root or has used su to become the superuser from another login.

## Creatively Using Partitions

As the system or LAN you administer becomes larger and more complex, there may come a time when you need to consider breaking down the file system. There are a number of reasons why this issue may arise. It is your own unique circumstances that determine where additional partitions would really help your system or LAN.

### Many Shell Accounts

In networks where there are a large number of accounts, it can be useful to break down the home portion of the file system further. For example, at an ISP you might have a partition mounted as /home/users where all paid user shell accounts are added, and another partition mounted as /home/staff where all staff member shell accounts are added. Keeping these items on separate partitions not only allows you to refine access permissions to these areas, but also lets you easily use separate quotas for users and administrative staff.

### Shared Departmental Data

In environments where there is a lot of work done in teams, it is useful to create individual areas where each team can easily access its collective data without making it open to the general public. One way to accomplish this task is to give each department its own partition for shared data. This partition would be accessible by all department members, a feature that can be implemented using secondary groups.

### Lots Of Small Files

A finite number of inodes is available for each partition. Perhaps you have many small files, such as data or temporary files from a software package. For example, let's say that one day you look at the partition's remaining inodes and find that you have very few left, and yet you have a lot of free space. You may need to give this batch of small files its own partition so it cannot hamper the rest of the file system's workings.

> **NOTE:** Although many people used to the MS-DOS or Windows world might consider defragmenting partitions under such circumstances, there are no defragmenting tools for Linux. There are no such tools because disk fragmentation does not cause appreciable problems in the ext2 file system.

### Protecting Your Data

It happens to everyone eventually. You go to boot the computer or access a file and discover that the file system is damaged. Sometimes you get lucky and it's only the /tmp directory that is bad. At other times, vital areas are corrupted. The deciding factor in whether this problem is a minor annoyance or a catastrophe is whether you have recent and reliable data backups.

### Introduction To Backup Schemes

There are a variety of backup schemes you can use. A backup scheme is a reference to your backup approach. There are a number of issues that affect how you determine what your backup scheme will ultimately be.

### Portion Of File System

Take a look at how easy each portion of the file system is to re-create. Be careful how you determine whether something is simple or not—what may seem simple now may not seem so easy five months later when you need to fix things after a crash.

It is possible to back up the entire file system if you have media large enough to hold it, or if you can span it among multiple media. However, as you will learn in the two sections on incremental backups in this chapter's Immediate Solutions section, it is not necessary to back up the entire file system every time. Items that administrators commonly back up most frequently are:

- The /home hierarchy
- Hierarchies that contain file server data, such as FTP or Web server file storage areas
- Any special directories containing program data
- Log files with data you cannot afford to lose, such as Web access data
- The /etc hierarchy, if you have configured many services lately

### Frequency

The frequency with which you make backups depends on your particular situation. You do not need to back up all items at the same frequency. Instead, you can have a separate backup set up for each important portion of the file system.

The main indicator of how often you need to back up a file system segment is how often the data changes, and how much of a problem it would be to lose data that is not yet backed up if a crash happens. If a month will not make much of a difference due to part of the hierarchy being fairly static, and the information there is not difficult to re-create, then that portion would not need to be backed up often. However, for data that can change at any moment and frequently—such as home directories and mail spools—a daily backup is highly recommended.

### Redundancy

If you keep one set of backup media and write over the media each time you back up, you miss out on the issue of redundancy. Perhaps an intruder crept in and you were unaware of him or her for a week. Those daily backups may contain corrupted files, and you have no way of checking them against anything older. This is only one reason to consider keeping redundant backups around. Other problems can occur because of program errors, user errors, or other situations that do not require malicious intent.

### Incremental Backup Scheme

Often, the goal of a backup is to be able to replace the entire system with a trusted copy if necessary. This goal brings up the issue of how much of the system to back up at a time. Technically speaking, it would be good to do a nightly full backup. Unfortunately, this task is not realistic.

Instead of doing a full backup every 24 hours, many people use a scheme of incremental backups. The aim of this scheme is to keep a copy of the file system as up to date as possible without doing daily full backups.

One incremental plan some might adopt is as follows:

1. Do daily backups together on a single storage media. A specialized shell script (see Chapter 20 for details on shell scripting) combined with automated reminders to be sure the media is in place and the script itself automated to run in early morning hours might back up:
   - Home directories
   - Web sites
   - Mail spool
   - Log files
2. Once a week back up items that change regularly, but not daily. Again you would use a separate storage media for this purpose, perhaps labeled “weekly” to distinguish it from the others. This backup would be larger, taking more time than a daily backup. On it you might have:
   - The entire daily backup scheme
   - The /etc hierarchy
   - The /opt hierarchy, if you install application packages there
   - The /usr/src hierarchy, if you work with source code regularly
3. Once a month, or once every two weeks, depending on how often your overall system changes, you could do a full file system backup. Be sure to label this media so you do not overwrite it with one of the more frequent backups.

> **NOTE:** This last step actually provides a very small amount of redundancy.

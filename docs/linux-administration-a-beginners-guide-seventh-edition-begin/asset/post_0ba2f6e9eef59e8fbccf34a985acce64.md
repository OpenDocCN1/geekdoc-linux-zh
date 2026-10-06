
# CHAPTER 31 Backups 765

## dump Command

### Description

- - level#
The dump level, where level# is a number between 0 and 9. Automatically sizes the tape. This is the default behavior of dump if -b, -B, -d, or -s (as documented later in this table) is not specified.

- - a
Uses bzlib library-based compression. Note that bzlib, while being an excellent compression scheme, comes at the expense of needing more CPU. If you use this method of compression, make sure that your system is fast enough to feed the tape drive without the drive pausing. Also note that this option might break compatibility with other UNIX systems.

- - j
Uses zlib library-based compression. Note that this option might break compatibility with other UNIX systems.

- - z

- - b blockSize
Sets the dump size to blocksize, which is measured in kilobytes. If there is more data to dump than there is tape space, dump will prompt you to insert a new tape.

- - B count
Specifies a number (count) of records per tape to be dumped. If there is more data to dump than there is tape space, dump will prompt you to insert a new tape.

- - f filename
Specifies a location (filename) for the resulting dumpfile. You can make the dumpfile a normal file that resides on another file system, or you can write the dumpfile to the tape device.

- - u
Updates the /etc/dumpdates after a successful dump.

- - d density
The density of the tape in bits per inch.

- - s size
The size of the tape in feet.

- - W
Displays what file systems to be dumped without actually performing any dumps. This is based on information in the /etc/dumpdates and /etc/stab files.

- - L label
Labels the dump with a name that can be read by the restore command.

- - S
Performs a size estimate without performing the actual dump.

## Table 31-2 Parameters for the dump Tool

(For example, you might know that the partition you are dumping is 2GB and the tape capacity is 5GB uncompressed.) In this situation, you can use a little trick to keep dump from calculating the tape size. Instead of dumping to the device, send the output to the standard output (stdout), and then use the cat program to redirect the dump to it. Using the example in the previous section, you would enter this command:

```
[root@server ~]# dump -0 -f /dev/sda1 cat >> /dev/st0
```

Since you're dumping the output to standard out, you can also use this opportunity to apply your own compression to the file stream instead of relying on hardware compression or the built-in compression command-line switches. For example, to use gzip to compress your dump, you'd type this:

```
[root@server ~]# dump -0 -f /dev/sda1 gzip --fast -c >> /dev/st0
```

> CAUTION It's not advisable to dump a file that is actively being used. The only way to be 100-percent sure that a file is not in use is by mounting it. Unfortunately, few people can afford the luxury of using a system for the time necessary to do a backup. The next best is to go through the unpleasant task of verifying backups on a regular basis. Verification is best done by testing to see if the restore program (discussed in the section "Using restoring," later in this chapter) can completely read the backup medium and extract files from it. It's tedious, and it's not fun. But a system administrator's head has rolled over bad backups—one of them!

## Using dump to Back Up An Entire System

The dump utility works by making an archive of one file system. If your system comprises multiple file systems, you need to run dump for every file system. Since dump creates its output as a single large file, you can create multiple dumps to a single tape by using a non-rewinding tape device.

Assuming we are backing up to a SCSI tape device, /dev/st0, we must first decide which file systems we are backing up. This information is in the /etc/fstab file. Obviously, we don't want to back up files such as /dev/cdrom, so we skip those. Depending on your data, we may or may not want to back up certain partitions (as swap and /tmp). Let's assume we have /dev/sda1, /dev/sda3, /dev/sda5, and /dev/sda6. To back up these using /dev/st0, compressing them all the way, we would issue the following series of commands:

```
[root@server ~]# mt -f /dev/st0 rewind
[root@server ~]# dump -0 -f /dev/sda1 gzip --fast -c >> /dev/st0
[root@server ~]# dump -0 -f /dev/sda3 gzip --fast -c >> /dev/st0
[root@server ~]# dump -0 -f /dev/sda5 gzip --fast -c >> /dev/st0
[root@server ~]# dump -0 -f /dev/sda6 gzip --fast -c >> /dev/st0
```

The first mt command makes the tape completely rewound and ready to accept data. Then come all dump commands run on the partitions, with their outputs piped through gzip before going to the tape. To make the backups go a little faster the --fast option is used with gzip. This results in compression that isn't as good as normal compression, but it's much faster and takes less CPU. The -c option on gzip tells it to send its output to the standard out. We then rewind the tape and eject.

## Using restore

The restore program reads the dump created by dump and extracts individual files and directories from them. Although restore is a command-line tool, it offers a more intuitive mode that lets you go through a directory structure from the tape. Table 31-3 shows the command-line options for restore utility.

| Option | Description |
| :--- | :--- |
| -i | Enables interactive mode for restore. The utility will read the directory contents of the tape and give you a shell-like interface in which you can move directories around and tag files you want to recover. When you've tagged all the files you want, restore will go through the dump and restore those files. This mode is handy for recovering individual files, especially if you aren't sure which directories they are. |
| -r | Rebuilds a file system. If you lose everything in a file system (via a disk failure, for instance), you can simply re-create an empty file system and restore all the files and directories of the dump |
| -b blocksize | Sets the dump's block size to kilobytes. If you don't supply this information, restore will figure this out for you. |
| -f filename | Reads the dump from file filename |
| -T directory | Specifies the temporary workspace (directory) for restore. The default is /tmp |
| -v | The verbose option; it shows each step restore is taking |
| -Y | In the event of an error, automatically retries instead of asking the user if she wants to retry.|

## Table 31-3 Command-Line Options for the restore Utility

A typical invocation of restore is as follows:

```
[root@server ~]# restore -ivf /dev/st0
```

This will pull the dump file from the device /dev/st0 (the SCSI tape device), print out each step restore takes, and provide an interactive session for you to decide which files from the dump get restored.

A complete file system is lost, you can re-create the file system using the mkfs.* command and then restore to populate the file system. For example, let's say your External Serial Technology (SATA) drive (/dev/sdb) fails, and you have a single partition on it (/dev/sdb1) formatted with the ext4 system. After replacing the failed drive with a new drive and partitioning it, we would re-create the file system:

```
[root@server ~]# mkfs.ext4 /dev/sdb1
```

> CAUTION To avoid data loss, make sure you are running any of the mkfs.* commands on the proper device.

Next, we have to mount the file system at the appropriate location. We'll assume this is the /home file system, so we type the following:

```
[root@server ~]# mount /dev/sdb1 /home
```

Finally, with the dump tape in the SCSI tape drive (/dev/st0), we perform the restoration using the following command:

```
[root@server ~]# cd /home; restore -rf /dev/st0
```

> TIP If you use gzip to compress your dump, you'll need to decompress it before restore can do anything with it. Simply tell gzip to uncompress the tape device and send its output to the standard out. Standard then be piped to restore, with the -f parameter set to read from standard (stdin). Here's the command:
```
[root@server ~]# gzip -d c /dev/st0 | restore -ivf -
```

## tar

Chapter 3 discussed the use of tar for creating archives of files. What wasn't discussed, however, is the fact that tar was originally meant to create archives of files onto tape (tar = tape archive). Because of Linux's flexible approach of treating devices as the same, we've been using tar as a means to archive and unarchive a group of files into a single disk file. Those tar commands could be rewritten to send the files to the tape instead.

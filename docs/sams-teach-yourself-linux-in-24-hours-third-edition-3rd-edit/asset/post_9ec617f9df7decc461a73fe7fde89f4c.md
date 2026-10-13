
3. Decide how often the system and individual files need to be backed up. You'll need to look at how often files change. If files change frequently, you may need to perform a backup every day. If you only make one or two configuration changes on occasion, you can easily backup the configuration files only when the change is made.

4. Select a storage media that will be used to store the file. If you have a few files to back up, you could just store them on a floppy disk. If you have more files, consider using a Zip drive or a recording CD-R/W drive. Linux has always worked well with tape drives. Even though tape backups might be on the way out, there is still a lot of use for older equipment.

5. Find a safe place to store the files. The safest place to store the backup media is at a location different from where the computer is located. This location also needs to be protected from fire and other hazards. A favorite storage place for many people is the safe deposit vault at their bank. Others may use a fireproof safe that is located at a secured storage facility. You may also want to keep a copy of the backups close by so that you can quickly restore lost files.

## Task: Performing a Simple Backup

The easiest way to back up a small number of files is to copy them onto floppy disks. The simplest method is to use the cp command. If the file is too large for a floppy, it can be compressed with the gzip command. When several files need to be backed up, create an archive with the tar command and compress the archive with the gzip command. Try this simple backup routine to copy a single file onto a floppy disk:

1. Place the floppy disk in the floppy disk drive. If you need help formatting the disk, go to Hour 7, "Moving Around the Filesystem." If you buy formatted disks in bulk from your favorite warehouse club, there's no need to format these disks to use them on your Linux system. Just put them in the drive and you're ready to go.

Before you can copy the file to the floppy, you need to mount the drive. To do so, use the mount command in the following format:

```
mount /dev/fd0 /mnt/floppy
```

2. Change the directory that contains the files you want to back up. Use the pwd command to see where you are, the cd command to move from directory to directory, and the ls command to view the list of files in a directory.

3. Copy a file to the floppy disk. Use the cp command in the following format:

```
cp filename /mnt/floppy
```

In Figure 10.1, our imaginary user, rusty, has copied a file to a floppy and then verified the contents of the floppy disk.

### FIGURE 10.1
Floppy disks are an inexpensive backup media and easy to maintain for a small number of files.

![](img/782ecfdc0b083a767896cc983e10427f_191_0.png)

> Another compression program that you may want to try is Bzip2. You can learn more about Bzip2 by reading the Bzip2 mini-HOWTO.

## Working with Storage Devices

You have several ways to store your backups. The choice you make depends on how much information needs to be stored, your computer budget, and how much time you want to take to configure devices on the Linux system.

Floppy disks have been used as a backup medium since the early days of computing. Floppy disks are inexpensive (and they come already formatted), easy to store, and every computer comes with a floppy drive, with the exception of some Macintosh setups that only have zip drives. Floppy disks are reasonably reliable, and you can lengthen the life of a floppy by storing it correctly. Floppy disks work well if you only have a few configuration files to back up, or if you only want to backup certain files in your home directory.

When storage space is a consideration, you may want to consider using removable disks on a Zip or Jaz drive. These devices allow you to store over 100MB of files and are more reliable than floppy disks. There is also a utility called GtkZip, shown in Figure 10.2, that can make managing Zip disks easier. GtkZip can also set a security level on Zip disks.

### FIGURE 10.2
Use your Zip drive to store backups with the GtkZip tool.

![](img/782ecfdc0b083a767896cc983e10427f_192_0.png)

Another backup alternative is a second hard drive. You can easily copy files (or the entire system) from the Linux drive to the spare hard drive. Because hard drives are not prone to failure until after considerable use, a hard drive that is only used to store backups may be a very reliable storage medium. Then when it’s time to restore the system, the hard drive can do it much faster than other media.

At about the same price as a hard drive is a read/write CD-R drive. This device allows you to make a one-time backup that cannot be overwritten. You should use a CD-R drive if you need a permanent record of your backup files. You can also archive as much as 650MB of files on a single CD.

Your choice of storage devices for your important backup files depends on how much room you’ll need to store files, what storage devices are already attached to the computer system, and how much your budget can afford a new storage device. Before you consider a storage device, you may want to read the following HOWTOs:

- If you need help setting up and using a Zip drive, read the "Zip Drive" mini-HOWTO. Most Linux distributions will automatically detect any parallel port versions of the Zip100 and will install the necessary drivers and create a mount point. The SCSI and IDE internal drives are common now and they are treated like hard drives. If you have a Jaz drive, read the "Jaz Drive" HOWTO.
- CD writers have recently become affordable to the average home computer user. The "CD-Writing" HOWTO explains the CD writers that are compatible with Linux, how to set them up, and what software you can use to write data files to a CD as well as how to record music onto a CD.
- If you want to back up your entire hard disk onto a second hard drive, read the "Hard Disk Upgrade" mini-HOWTO. This procedure allows you to just swap hard disks if the primary hard disk fails.

## Task: Saving Disk Storage Space

One way to reduce the size of a file is to use a compression utility. You may have a file that is too large to fit on a floppy disk. If so, use the gzip command to compress the file enough so that it fits. You may have files in your home directory that you use infrequently. If so, save some space and compress the files. Try these compression tricks:

1. Compress the file by using the gzip command as follows:

```
gzip -v filename
```

This command tells gzip to compress the file and to display the compression percentage for the file. The original file is replaced with the compressed file, and the extension .gz is added to the end of the filename. For example, user rusty has three files that are not used often and that take up space (the file listing appears in Figure 10.1). When rusty executes the command

```
gzip -v 23FIG??.pcx
```

the following appears on the screen:

```
23FIG01.pcx: 76.1% -- replaced with 23FIG01.pcx.gz
23FIG02.pcx: 76.1% -- replaced with 23FIG02.pcx.gz
23FIG03.pcx: 76.1% -- replaced with 23FIG03.pcx.gz
```

This listing shows the original filename, the percentage of compression, and the new filename of the compressed file.

2. Uncompress the file by using the gunzip command as follows:

```
gunzip filename
```

For example, if rusty wanted to decompress the file named 23FIG01.pcx.gz, he would type this:

```
gunzip 23FIG01.pcx.gz
```

The file is restored to its original, uncompressed state and can be used by an application that can read files of that type.

3. Compress every file in a directory by using the gzip command as follows:

```
gzip -rv directorypath
```

If rusty wants to compress the contents of the corresp subdirectory located in the user home directory, the following command would be used:

```
gzip -rv /home/rusty/corresp
```

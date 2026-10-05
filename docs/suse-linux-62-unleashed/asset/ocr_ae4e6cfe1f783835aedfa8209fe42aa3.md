you must use a full pathname (such as /root/backup.tar) when specifying the archive name.

FIGURE 20.9
Use YaST's backup dialog box to name your archive, use compression, and/or create a table of contents file.

![](bbox=[0.235, 0.185, 0.735, 0.42])

yast will then back up your system and create the archive and contents file.

# # Restoring Files

Backing up files is a good thing, but backups are like an insurance policy. When it is time for them to pay up, you want it all, and you want it now! To get the files, you must restore them. Fortunately, it is not difficult to restore files with either tar or cpio. The following command restores the file /home/alana/bethany.txt from the current tape in the drive:

```
$ tar -xpf /home/alana/bethany.txt
$ cpio im `bethany.txt` < /dev/rmt0
```

The -p in tar and the -m in cpio ensure that all the file attributes are restored along with the file. By the way, when you restore directories with cpio, the -d option creates subdirectories. The tar command creates subdirectories automatically.

# # What Is on the Tape?

When you have a tape, you might not know what is on it. Perhaps you are using a multiple-level backup scheme and you don't know which day the file was backed up. Both tar and cpio offer a way of creating a table of contents for the tape. The most convenient time to create this TOC file, of course, is during the actual backup. The two lines show how to perform a backup and, at the same time, create a table of contents file for that tape:
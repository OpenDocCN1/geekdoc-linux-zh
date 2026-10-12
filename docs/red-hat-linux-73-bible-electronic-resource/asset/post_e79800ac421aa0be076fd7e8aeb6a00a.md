
wasteful of storage space on the backup tape, but it will save a lot of time and effort should there be a need to restore the file system.

For example, let us imagine that your hard drive crashed on Friday. After replacing the hard drive, you can restore the entire file system in two steps: restore the full backup from the prior Sunday and then the most recent incremental backup from Thursday. We can do this because Thursday's backup contains all of the files from Monday, Tuesday, and Wednesday's tape as well as the files that changed after that. If the dump levels had progressed in positive order (level 1 for Monday, level 2 for Tuesday, and so on), all of the incremental backups would have to be restored in order to restore the file system to its most current state.

## Automating Backups with cron

You can automate most of your backups with shell scripts and the cron daemon. Use the su command to become root, and then cd to the /usr/local/bin directory. Use any text editor to create a shell script called backups.sh that looks similar to the following:

```bash
#!/bin/sh
#
# backups.sh - A simple backup script, by Thad Phetteplace
#
# This script takes one parameter, the dump level.
# If the dump level is not provided, it is
# automatically set to zero. For level zero (full)
# dumps, rewind and eject the tape when done.
#
if [ $1 ]; then
    level=$1
else
    #
    # No dump level was provided, so set it
    # to zero
    #
    level="0"
fi

/sbin/dump $level'uf' /dev/nrft0 /
/sbin/dump $level'uf' /dev/nrft0 /home
/sbin/dump $level'uf' /dev/nrft0 /var
/sbin/dump $level'uf' /dev/nrft0 /usr

#
# If we are doing a full dump, rewind and eject
# the tape when done.
#
if [ $level = "0" ]; then
# Note: We should replace this with the /bin/st command
# instead if we ever switch to a SCSI tape drive.
#   /bin/mt -f /dev/nrft0 rewind
      /bin/mt -f /dev/nrft0 offline
fi
```

You may choose to change the partitions being backed up to match your situation, but this script should otherwise work quite well for you. After saving and exiting the editor, change the permissions on the file so that it is executable only by root:

```bash
# chmod 700 backups.sh
```

You can now back up your entire system by running the **backups.sh** script when logged in as root. The script accepts the dump level as its only parameter. If you leave the parameter off, it will automatically assume a level zero dump. Thus, the following two commands are equivalent:

```bash
# backups.sh
# backups.sh 0
```

You may need to customize this script for your situation. For example, I am using the tape device **/dev/nrft0**. You may be using a different tape device. Whatever device you use, you should probably use the version of its device name that begins with a `letter n.` That tells the system that after it finishes copying data to the tape, it should *not* rewind the tape. As an example, I used **/dev/nrft0** instead of **/dev/rst0** in the preceding script. If I had used **/dev/rst0**, each successive incremental backup would have overwritten the previous one.

Other things that you may change in this script include the partitions being backed up and the dump level at which the tape is ejected. It is not uncommon to eject the tape after the last incremental backup just before performing a full backup.

The most useful thing about this script is that you can easily configure your system to run it automatically. Simply add a few lines to the root **crontab** file, and the cron daemon will invoke the script on the days and times specified. While logged in as root, enter the **crontab** command with the `-e` option:

```bash
# crontab -e
```

This brings up the root **crontab** file in an editor. Add the following lines at the end of the file:

```cron
0 22 * * 0 /usr/local/bin/backup.sh 0
0 22 * * 1 /usr/local/bin/backup.sh 9
0 22 * * 2 /usr/local/bin/backup.sh 8
0 22 * * 3 /usr/local/bin/backup.sh 7
0 22 * * 4 /usr/local/bin/backup.sh 6
0 22 * * 4 /usr/local/bin/backup.sh 5
0 22 * * 5 /usr/local/bin/backup.sh 4
```

Save and exit the file. The cron daemon will now run the backup script at 10:00 p.m. (22:00 in military time) every day of the week. This example implements the dump schedule outlined earlier. A full dump is performed on Sunday, and the tape is ejected when it is done. A new tape should be loaded on Monday, and then incremental backups will be written to that same tape for the rest of the week. The next full dump will be written to the end of that tape, unless someone is around on Sunday to eject and replace the tape before 10:00 p.m.

## Restoring Backed Up Files

The *restore* command is used to retrieve files from a backup tape or other media. You can use *restore* to recover an entire file system or to interactively select individual files. It recovers files from the specified media and copies them into the current directory (the one you ran the *restore* command in), re-creating subdirectories as needed. Much as with the *dump* command, the first parameter passed to the *restore* command is a list of single character option codes, as shown in Table 13-5.

### Table 13-5: Restore Command Options

| Restore Options | Description |
|---|---|
| r | Restore the entire dump archive. |
| C | Compare the contents of the dump file with the files on the disk. This is used to check the success of a restore. |
| R | Start the restore from a particular tape of a multitape backup. This is useful for restarting an interrupted restore. |
| x | Extract only specific files or directories from the archive. This option takes one argument, a list of files or directories to extract. |
| t | List the contents of the dump archive. If a file or directory is given as an argument, list only the occurrence of that file, directory, or anything within the directory. |
| I | Restore files in interactive mode. |
| b | Specify the block size of the dump in kilobytes. This option takes a numeric argument. |
| D | Specify the name of the file system to be compared when using the C option. The file system name is passed as an argument. |
| f | Specify the name of the dump archive to restore from. This option takes an alphanumeric argument. |
| h | If this option is specified, *restore* re-creates directories marked for extraction but will not extract their contents. |
| m | Files are extracted by inode number instead of name. This is generally not very useful. |
| N | Instead of extracting files, print their names. |
| s | Specify the dump file to start with on a multiple file tape. This takes a numeric argument. |
| T | This tells *restore* where to write any temporary files. This is useful if you have booted from a floppy (which has no space for temporary files). |
| v | Run in verbose mode. This causes *restore* to print information about each file as it restores it. |
| Y | The *restore* command will always continue when it encounters a bad block, rather than asking you if you want to continue. |

### Restoring an entire file system

Let us return to our earlier example of the Friday disk crash. You installed a shiny new hard drive and your backup tapes are in hand. It is time to restore the files. For the purpose of this example, I am assuming that the crashed drive contained only the /home partition and that the Red Hat Linux operating system is still intact. If the crashed drive had contained the Red Hat Linux operating system, you would first have to reinstall Red Hat Linux before restoring the backup.

Before any files can be recovered to your new hard drive, an empty file system must be created on it. You will use the *mkfs* command to do this. The *mkfs* command can accept a variety of parameters, but usually you only need to supply the name of the device to create the file system on. Thus, to prepare the new hard drive type:

```bash
# mkfs /dev/hda6
```

Alternatively, because our /home drive is listed in the /etc/fstab file, we can simply specify the mount point /home *mountpoint* and *mkfs* will figure out the correct device. Thus, the preceding command could be replaced with this:

```bash
# mkfs /home
```

> **CAUTION:** You should, of course, exercise extreme caution when using the *mkfs* command. If you specify the wrong device name, you could unintentionally wipe out all data on an existing file system.

After creating a file system on your new disk, mount the partition to a temporary mount point.

```bash
# mount /dev/hda6 /mnt
```

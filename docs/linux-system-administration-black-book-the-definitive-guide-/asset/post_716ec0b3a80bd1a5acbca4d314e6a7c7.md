
## Table 3.8 Popular flags used with the fsck command.

| Flag | Purpose |
| :--- | :--- |
| -r | Checks with the person running the command before making repairs, instead of making them automatically. |
| -t | Signals that the person running the command will specify the only file system type to check. |
| -A | Checks every file system defined in /etc/fstab. Best used in conjunction with -t to ensure that only ext2 file systems are checked. |
| -V | Runs in verbose mode. |

# Backing Up And Restoring File System Structure

Sometimes it is worthwhile to back up the structure of your file system separate from the file system itself. This information is immensely useful to have if you accidentally alter permissions or ownerships in important sections of the file system, or a misguided program does it for you. Trying to backtrack and fix things without a roadmap is not pleasant.

## Backing Up File System Structure

Make a backup of the file system structure in the following manner:

- 1. Because you want to include the entire file system, type “cd /” to go to the root of your file system.
- 2. Type “ls -IR > listing” to save the file system structure to the file “listing”.
- 3. If desirable, compress the listing by typing “gzip listing”, which gives you a file called listing.gz.

TIP: This method is also how the large Linux FTP sites are able to offer a file containing the listing of their directories. They just begin the command from the top of the FTP file system, not from the machine’s file system.

Related solutions:

| Related solutions: | Found on page: |
| :--- | :--- |
| Creating Gzipped Files | 108 |
| Creating Z Compressed Files | 108 |
| Opening Or Creating Tarballs | 110 |

## Restoring File System Structure

Restoring the structure of your file system after a “glitch” is not as easy as just typing a single command. However, there is a straightforward process to follow:

- 1. Locate the file containing your file system listing, for example, /listing.gz.
- 2. Unzip the file if necessary by typing “gunzip listing.gz”, which produces the file listing.
- 3. There are a number of ways to approach this issue from here; I will illustrate one of them. Type “less listing” to display the beginning of the file. The reason I chose the less program instead of more is that less highlights search terms when they are found.
- 4. Choose a logical starting point within the file system. (You should know where the glitch hit. If not, you still must have a reason for starting this process.)
- 5. Determine a distinctive chunk of text to search for, so that you do not have to page through the listing.
- 6. Type “/text”, where text is the search term, and press Enter.
- 7. If the term does not match what you were looking for, type a slash (/) and press Enter once again. Continue this until you find the correct entry.
- 8. In another terminal or terminal window, type “ls -l entry” to list the full information for the item you are trying to fix.
- 9. Compare the information between the listing file and the current entry listing. Use the chmod, chown, and chgrp commands, respectively, to fix any problems.
- 10. Return to Step 4 for the next item you need to fix.

NOTE: How useful the backup file system listing is depends on how recent it is. Be sure to back up often.

Related solutions:

| Related solutions: | Found on page: |
| :--- | :--- |
| Creating gzipped Files | 108 |
| Creating Z compressed Files | 108 |
| Opening Or Creating Tarballs | 110 |

# Back Up File Systems

One of the most important things any system administrator can do is set up some form of backup routine. Only if there are absolutely no files on a machine that you might want to keep should you ignore this issue. Although the specifics differ here and there, there is a general process to follow when creating a backup routine:

- 1. Determine what type of information you want to back up, and create a backup scheme, as discussed in “Protecting Your Data” in the In Depth section.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_110_0.png)

- 2. Determine which media you want to use to store the particular backup segment in question, with the help of “Backup Hardware” in the In Depth section.
- 3. Which media you choose determines what software you need in order to create the backups. A map of which media requires which software is given in Table 3.9.
- 4. Load the kernel module or install the driver that you need for the media.
- 5. Install the software if necessary.
- 6. If you are using special software, read the documentation and learn how to use it. Otherwise, read the **tar** man page and see Chapter 4 for various tips on how to use the **tar** package.
- 7. Build your archive onto the media.
- 8. Verify that the archive worked. You know a backup worked if you are able to pull any files back off of the media. See the section “Restoring File Systems From Backup” for how to accomplish this task.
- 9. Clearly label the backup media.
- 10. Store the backup media in a safe place.

## Table 3.9 Drivers and outside software necessary for various backup media.

| Media | Driver | Software |
| :--- | :--- | :--- |
| CD writer or CD rewriter | cdrecord or cddaof | There are a number of programs out there that you can use to write the data to the CD. See the CD writer HOWTO at www.linuxdoc.org/HOWTO/CD-Writing-HOWTO-1.html for more information. |
| DVD writer or DVD rewriter | Universal Disk Format (UDF) file system driver, hardware driver | Program that can write to both ISO9660 and UDF. This technology is not quite ready for production use as yet. Watch your favorite Linux news sites for more information. |
| Floppy disk | No special drivers | No special software is necessary. |
| LS-120 | pf driver | No special software is necessary. |
| RAID | Kernel patch | Raidtools software. |
| Removable rack hard drive | No special drivers, but special equipment needed to swap things out | No special software is necessary. |
| Tape drive | ftape driver, which is already installed in most distributions | No special software is necessary, but sometimes it is worthwhile to have. |
| Zip disk | ppa driver (kernel module) | No special software is necessary. |

Related solution:

| Related solution: | Found on page: |
| :--- | :--- |
| Creating **tar** files | 109 |

## Restoring File Systems From Backup

Restoring a file system, or part of a file system, is a process that depends somewhat on what software you are using. What follows is the general process for restoring files from backup:

- 1. Locate the media containing the data you need to restore.
- 2. Mount the media onto the file system.
- 3. Determine how much of the information on the media you want to restore.
- 4. Determine how much of the information your software (**tar** or another package) forces you to restore. You may not be able to work one file or directory at a time.
- 5. Use the **tar** application, as discussed in Chapter 4, or the software package you used to create the backup in order to extract the needed files.
- 6. Test the file system to ensure that the restoration succeeded.
- 7. Unmount the media.
- 8. Return the media to proper storage.

Related solution:

| Related solution: | Found on page: |
| :--- | :--- |
| Opening **tar** files | 110 |

## Moving File System Portions Onto Partitions

System needs tend to change over time. You may find after a while that you want to move a file system hierarchy onto its own partition instead of leaving it on root or on another partition. To accomplish this task, do the following:

- 1. Install the new hard drive if necessary.
- 2. Create the new partition using a tool such as `fdisk`.
- 3. Rename the current version of the hierarchy using the `mv` command. For example, `mv /home/old-home`.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_112_0.png)

- 4. Create a new directory with the original name using the `mkdir` command. For example, `mkdir /home`.
- 5. Mount the partition onto the now empty mount point, which is the new directory you just made.
- 6. Use the `cd` command to change into the moved version of the hierarchy. For example, `cd /old-home`.
- 7. Use the `cp` tool in the form `cp -rp . newdir` to recursively copy the files—along with their owner, group, permission, and timestamp settings—from the current location to the new partition. For example, `cp -rp . /home`.
- 8. Use the `cd` command to change to the new partition. Take a few moments to ensure that everything copied over properly. Try running programs and editing files and generally putting the partition through its paces.
- 9. Once you're sure that the transfer went well, delete the old version with the `rm` command in the format `rm -r olddir`. For example, `rm -r /old-home`.

WARNING! Double-, triple-, and quadruple-check that you have typed this command properly before you press Enter. The last thing anyone needs is to delete the wrong portion of the file system!

- 10. See the section “Adding Permanent Media” on how to add this partition to `/etc/fstab`.

## Adding And Removing Media To The File System

There are two different approaches to adding and removing media, depending on its purpose. Temporary media, such as floppy disks and CD-ROMs, are often added and removed in short periods of time. However, if you are adding new partitions that you want to permanently make part of the file system, then you will use a different approach.

### Adding Temporary Media

To add media temporarily to the file system, do the following:

- 1. Physically add the media to the file system. This act may involve putting a floppy disk in a drive, a Zip disk in a Zip drive, or a CD-ROM in the CD-ROM bay.
- 2. Determine which device driver pertains to the media. Table 3.10 lays out the paths for commonly used drivers.
- 3. Determine which file system is used on this device. Table 3.11 lays out the file system formats commonly used with temporary media in Linux.

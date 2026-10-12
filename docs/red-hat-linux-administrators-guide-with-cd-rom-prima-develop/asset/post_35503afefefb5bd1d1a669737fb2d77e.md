
Once the backup is complete, the file is readable by root and is found in ASCII text format. You can modify the file manually so that restores will read only those files that you want to back up. No special commands are needed to edit this file.

Because both dump and restore require access to the partition's device, root permission is usually required. For example, if performing a dump of the root directory in /dev/hda1, normally you only would have permission to that particular partition. Therefore, the dump and restore binary files are located in the /sbin directory, a location similar to that of the shutdown command and other high-level commands that are not normally found in root's path. I make it a practice simply to state the full pathname to these commands when executing a dump or restore routine in order to minimize the directories located in root's path.

You can run dump locally or remotely. In other words, you can dump files from the hard drive to an attached tape drive, or you can just as easily dump them to a backup machine with a tape drive. However, to dump files remotely, you need root access to the other machine as well. Linux provides a method for achieving root access on the backup machine. Years ago when most networked machines were run by trusted individuals and security concerns were minimal, developers created the .rhosts file. In this file you can enter the names of trusted machines that can have remote access to your machine. By placing the name of machine requiring backup in the /root/.rhosts file of the backup machine, you can grant a remote user root access remotely.

### CAUTION

If you want to allow the machine quasi.mydomain.com access to backup.mydomain.com, you would enter the names of each respective machine—in this case, quasi.mydomain.com—that will be backed up into the /root/.rhosts file, thus allowing root read/write access to the tape drive device on the backup machine. You would also need to enable rsh and login in the /etc/inetd.conf file on the remote backup machine. These programs are normally considered security holes and are disabled if internal security is an issue.

You should replace rsh with ssh and thus eliminate many of these security issues. However, rsh and rlogin will operate adequately if you are on a secure network—that is, if your system is protected by a firewall or you otherwise feel confident in your system's security.

### NOTE

To keep all servers that require periodic backup onto the archival machine relatively secure, you can use the chmod command to set the /root/.rhosts file on the backup server to 600, thus enabling only the root user to read and write to the file. Both rsh and rlogin still represent a serious security hole, but only to the backup servers themselves.

You can specify several options for the dump command when setting the type of backup procedure. You must first indicate what level of backup you want to execute. Full backups usually take the -0 option. (Remember, Linux begins its counting with the number 0.) Once a full or primary backup is completed, dump will write to the /etc/dumpdates file, and when a sequential -1 backup is performed, dump will search through /etc/dumpdates and compare the files requested for this backup procedure. You can also change the block size, density, and feet of any type of tape when backing up.

Listing 9.2 shows the syntax that I normally use for a standard dump that backs up the entire contents of my Linux box. You can place similar coding into a simple executable script much as I have done in this example.

### Listing 9.2 A Sample Script Used for Backing Up Multiple Partitions onto a Single Magnetic Tape

```bash
#!/bin/bash
# Back up all the partitions
#
/sbin/dump -0uf /dev/nst0 -b 64 -B 4000000 -L "*" /dev/hda1 &&
/sbin/dump -0uf /dev/nst0 -b 64 -B 4000000 -L "/home" /dev/hda7 &&
/sbin/dump -0uf /dev/nst0 -b 64 -B 4000000 -L "/opt" /dev/hda8 &&
/sbin/dump -0uf /dev/nst0 -b 64 -B 4000000 -L "/usr" /dev/hda5 &&
/sbin/dump -0uf /dev/nst0 -b 64 -B 4000000 -L "/usr/local*" /dev/hda6 &&
/sbin/dump -0uf /dev/st0 -b 64 -B 4000000 -L "/var" /dev/hda10
# End of file
```

The -f option tells dump where to place the files. In this case, it is the remote tape otherwise known as device /dev/nst0 or /dev/st0. The n prefix simply informs the system not to rewind the tape once the backup is complete, but to continue with the next partition.

In this instance, I am using DDS-2 4.0 gigabyte tapes, which are more than sufficient for an entire backup of all pertinent data. If all the partitions are more than 4 gigabytes, you can limit the directories in a given backup routine. Or, you can allow the backup to span more than one tape. The dump command will prompt you for an additional tape once it has reached the physical end of the media and will continue its backup on the second, third, and fourth tape as necessary.

### Remotely Dumping Files

Performing backups to a remote machine is a simple matter of prefacing the device name with the remote machine name and a colon. The following example shows how to back up the directories of a domain name server or DNS server onto the remote backup machine:

```bash
#!/bin/bash
# Back up all the partitions on nsl.mydomain.com.
/sbin/dump -0uf backup.mydomain.com:/dev/nst0 -b 64 -B 4000000 -L "/" /dev/hda1 &
/sbin/dump -0uf backup.mydomain.com:/dev/st0 -b 64 -B 4000000 -L "/var" /dev/hda5
```

I call the preceding script /dodump and have made it an executable file—that is, I used chmod to set it to 700, and have placed it in the / (root) partition of each machine that I want to back up.

Now let's closely examine each section of the previous script:

- The first section is the absolute path for the dump command. Normally, dump is not located in root's path. Hence, it helps to define the absolute path.
- This section is where you define the types of backups to be performed—that is, whether it is to be a full backup or an incremental backup. Because each full backup usually requires less than an hour to be completed, I like to do a full backup, or a 0 level, each time. If time and CPU cycles are of the essence, you can do a level 1–9 backup, which will back up only those files that have changed since the previous backup.
- The -u option instructs dump to update the /etc/dumpdates file after a successful backup. You can check this file to see when the last backup was completed. The -f option tells dump the name of the device to which it should transmit the data. From this device the dump command passes the dump data to the backup machine and then onto device st0 or st0.0.
- The next series of options indicate the blocking factor. The -b 64 option specifies that the data should be backed up in blocks of 64 kilobytes. This is fairly standard and is required for larger tapes.
- The next option, -B 4000000, specifies the size of the tape. Normal 120 meter DDS-2 tapes hold 4 gigabytes of data uncompressed.
- The -L option allows you to affix a label to the partition you are backing up, hence the / suffix. This option is limited to only 16 characters, so I like to use only the partition name. This feature is a new addition to the latest release of dump. It came standard with the Solaris ufcdump program and has just now found its way to Linux dump/restore.
- You must next define the partition that you want to back up. You can feasibly give this option the name of the partition itself such as /usr/local or /var, but I prefer to define the device name of the partition. This ensures that the backup will be done correctly.
- You may also need to place a double ampersand at the end of each line to make certain that the program does not overwrite the directory that you just finished backing up. Normally you would use a semicolon (;) to differentiate between each backup command and prevent it from over-writing the previous dump execution. Dump dictates that the double ampersand be used between multiple backup calls when saving to a single tape.

Now look at the sample output of a backup routine. The dump command's output tends to be verbose to ensure that the backup is done correctly. You can just as easily pipe this output to a file if you want to save it for future reference. Redirecting the output to an appropriately named log file by adding a redirect symbol to the end of the expressions, for example, `> my_saved_file.txt`, accomplishes this same task and allows you to peruse the output at a later time.

```bash
/sbin/dump -0uf backup.ksl.com:/dev/st0 -b 64 -B 4000000 -L "/var" /dev/hda5 >> /tmp/backup.log.000508
```

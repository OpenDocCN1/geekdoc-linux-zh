
being used for the remote shell. On each line of the `.rhosts` file, enter the names of each machine and user ID that are allowed to connect without providing a password.

## VERIFYING THE BACKUP IS SUCCESSFUL

The only real way to ensure that a backup was successful is to actually restore the data back on the system. Some people like to list the table of contents of the tape. If you are using shell scripts to run your backups, then *always* check the *return code* of the backup command (specified by `$?`)! If the *return code* is not 0, then the backup was *not* successful. A technique that I like to use is to create a dummy file on the system just prior to initiating the backup. When the backup is complete, I remove the dummy file, rewind the tape, and restore the dummy file back onto the system. Using this method ensures that the tape is good and that data can be extracted from it. This, of course, is not a full restore of the data, but it is better than a table of contents listing. Should you ever have any backup or restore fail, you should *always* check the error log (*errpt*) for any `rmt` errors.

## MAKING A COPY OF A TAPE

The `tcopy` command is used to make a copy of a magnetic tape. The source tape must have the normal EOF double tape markers to specify the end of tape. The EOF markers tell the `tcopy` command to stop copying. The `tcopy` command takes as input source and destination tape devices as command parameters. As an example, to copy from the streaming tape device `/dev/rmt0` to the tape device `/dev/rmt4`, you use the following command:

```
# tcopy /dev/rmt0 /dev/rmt4
```

If only the source tape device is specified on the command line, then the `tcopy` command prints information about the size of the tape records and the tape files. If that tape is empty or full, you will not get the tape or command line back until `tcopy` gets to the physical end of the tape.

## WHAT'S ON THAT TAPE?

Have you ever had a backup tape for which you had no clue how the archive was made? This is a typical problem, but there is a way to determine not only the archive format but also the tape drive block size that was used to make the tape.

The first step is to save the current tape block size using the `lsattr` command:

```
# lsattr -El rmt0 | grep block_size
```

This command assumes the tape drive is /dev/rmt0. The second column in the output is the current tape drive block size. If it is 0, then the tape is set to variable length, which is what we want for this procedure. If the block_size is anything other than zero, then write down the value for future reference. To set the block size to variable length, issue the following command:

```
# chdev -l rmt0 -a block_size=0
```

assuming the tape drive is /dev/rmt0. The next step is to extract the first 128K block of data from the tape. To accomplish this, use the dd command and set the block size to 128K:

```
# dd if=/dev/rmt0 bs=128k of=/tmp/tape.out count=1
```

Using the output file that we created, /tmp/tape.out, we can determine the block size that was used to make the tape by doing a long listing of the file. The size of the file is the tape block size:

```
# ls -l /tmp/tape.out
-rw-r--r--  1 root    system    1024  Feb 21 10:08 tape.out
```

In this example, the tape block size is 1024. To find the format of the data on the tape—for example, tar, backup, or cpio—you use the file command.

```
# file /tmp/tape.out
tape.out:        tar archive
```

This archive is a tar archive and was backed up with a tape block size of 1024.

If you changed the tape block size to variable length before, you can now change it the desired tape density using the following command:

```
# chdev -l rmt0 -a block_size=new_value
```

## CHECKLIST

The following is a checklist for the key points in system backup:

- The **mkssys** command is used to create a bootable system image of the rootvg volume group. However, this command doesn't back up other volume groups that might exist on your system.
- For non-rootvg volume groups, use the **savevg** command to save an entire volume group and its structure in a format that can be easily restored with the **restvg** command.
- Use the **backup** and **restore** facility to back up by filename or by i-node.
- Even in the single-user environment, it's a good idea to develop a discipline for *performing regular backups*.
- When creating a backup policy, some items you must consider are which file-systems to back up and how often, whether to back up whole file-systems or mounted or unmounted, full and incremental backup schedules, media types and media rotation schedules, bandwidth considerations for network-based backups, the backup program and format, and restore procedures.
- Root volume group file-systems, such as `/usr` and `/`, tend to be static in nature and may be replicated on a number of machines. Thus, they may not require dumping as often as dynamic file-systems such as those containing user home directories and work areas.
- To guarantee data integrity, a file-system should be synched and unmounted during backup. If your environment requires 24 × 7 uptime, you can perform backups while a file-system is mounted and in use, but you run the risk of missing data block updates in progress during the backup.
- An efficient full/incremental backup strategy is to run a full backup once a week, and on the other days run an incremental backup to back up everything that changed since the last full backup.
- Complex backup sequences can be tracked through the use of the `/etc/dumpdates` file. The *dumpdates* file records the file-system, backup level, and time stamp.
- Periodically test your backup sets by performing a restore operation. Verify that the backup media is good and that the data is valid.
- Periodically rotate a full set of backup media off-site.
- Regularly cycle the media through a physical cleaning and validation check. This includes periodic maintenance and cleaning of the backup devices.
- AIX 5L adds the ability to back up data onto DVD or CD-ROM drives. However, for a CD-ROM, you need 645MB available actual file-system space, and for a DVD, you need 8.8GB of file-system space.
- The `tar`, `pax`, and `cpio` utilities can be used when portability is an issue. Either `pax`, `tar`, or `cpio` will allow you to copy files and directory trees between systems, preserving UIDs and permissions.
- Use `cpio` on SYSV UNIX machines where `tar` is not available.
- If you have the disk space to spare, you can copy a logical volume using the `cpio` command. This mechanism could be used to create a file-system copy for backup, leaving the primary copy online.
- You can use the network to back up remote workstations onto machines equipped with high-capacity tape drives with the `rdump` and `restore` commands, which are similar to the `backup` and `restore` commands.
- You can also perform network-based backups using the remote shell command `rsh` with one of the local backup or copy commands.
- Use the `tcopy` command to make a copy of a magnetic tape.

![](img/82f851021955589d82b22750fb3b1646_574_0.png)

![](img/82f851021955589d82b22750fb3b1646_575_0.png)

# CHAPTER 26

## System Monitoring and Tuning

Performance monitoring and tuning could be the phrase that sends more systems administrators into hysterics than any other. Trying to figure out why a system is suddenly performing poorly is not a particularly enjoyable task. There are so many different places to begin looking for trouble: you can ask yourself “Do I need more memory?” or “Do I need more processor power?” or “Are my disk drives working too hard?” Fortunately for us, AIX 5L has many tools available to assist us in answering these questions.

## KNOW YOUR WORKLOAD

Knowing your workload is one of your most important duties as an AIX systems administrator. What we mean by this is that you know the system, its hardware configuration, and what applications are running on it better than anyone else. Therefore, it will be your responsibility to know what events are running at particular times of the day that could affect the performance of the system. For example, let's say you are in the distribution business, and you have a system that is running some type of warehouse or inventory control software. It would be logical to assume that the system will be busier early in the morning and late in the evening, as distribution trucks leave the warehouse at the beginning of their delivery routes and return at the end. During other times of the day, the system would probably not be under as heavy a workload.

## AIX OPERATING SYSTEM CHARACTERISTICS

The basic characteristics of the operating system that we can most easily monitor and adjust are the CPU load, the system memory, disk input and output, and the network the system is attached to.

## CPU Scheduling

CPU scheduling refers to the act of assigning priorities to processes on the system. The process of accomplishing this can be as simple as using the **nice** command to raise or lower the priority of a single process, or as complex as using the **schedtune** command to tune the CPU scheduler itself. In service level 2 of AIX 4.3.3, and continuing on in AIX5L, IBM has incorporated a new performance-tuning feature known as Workload Manager. This allows for a policy-based approach to resource management. Using Workload Manager, like tasks are grouped together into classes, and priorities for system resources are assigned to those classes. If you are interested in taking this type of approach to system performance tuning, IBM has a Redbook on the subject, *AIX 5L Workload Manager* (*WLM*). The catalog number for this Redbook is SG245977, and it is available online at http://www.redbooks.ibm.com/.

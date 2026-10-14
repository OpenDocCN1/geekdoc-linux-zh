
## Database Backups: Cold or Hot?

When you are backing up files belonging to a database application, such as Oracle or MySQL, or applications that constantly keep certain files open, such as Lotus Notes, you need to give some extra thought than you would when backing up typical documents, such as OpenOffice files. There are two methods of performing a backup on a database: cold and hot. In a **cold backup**, an application is taken offline, which means there’s no user access to the data, and the data is backed up; this is the way backups are normally done. In a **hot backup**, on the other hand, the application remains online, and user access is retained while the backup is performed.

A cold backup is usually the optimal solution for those applications that can tolerate multiple hours of downtime to perform the backup. Some applications that used to be backed up cold have now grown so large that the backup cannot be completed during the allotted time window. If a cold backup is still desired, one way is to take a point-in-time “snapshot” of the data, and within a matter of minutes (depending on the size of the data files involved), the application is brought online. The snapshot can then be mounted back onto the application server, or mounted directly to the backup server, and backed up. Total downtime for the application in such a case is the time required to stop the application, perform the snapshot, and then restart the application.

> **NOTE**
>
> To take a snapshot of an application’s database, either you need an application that provides this feature, or you need to obtain additional software and/or hardware.

> **TIP**
>
> It is possible to create a *snapshot device* that is an alias for an existing Logical Volume (LV). The snapshot device, which can be accessed read-only, contains a point-in-time image of the LV; in other words, while applications continue to change the data on the LV, this logical device contains the unchanging image of the LV at the time when the snapshot was created. This makes it possible for you to do a consistent backup without shutting anything down or using any special software. This method is independent of any software because it happens in the LV Manager abstraction layer. SUSE has included a Logical Volume Manager since SUSE LINUX 6.3. For details on performing backups using LVM snapshots, see http://www.tldp.org/HOWTO/LVM-HOWTO/index.html.

If you want to perform a hot backup on an application that has constantly open files, the application must have a hot backup feature, and the backup software needs hot backup support for the specific application. Generally speaking, in hot backup mode, instead of writing to the live data, the application queues up the updates in a special file so the backup software can get a complete backup of the database. The special file is backed up next. After this is done, the application is then allowed to apply the queued-up changes to the database, thus bringing everything up to date.

Therefore, to decide whether you should perform a cold or hot backup of your database application files, you need to take the following factors into consideration:

- Can the application data files be backed up cold and not violate their integrity? If not, does the application have a hot backup feature?
- Does your backup software support the hot backup option of that particular application?
- How much of a downtime window do you have to back up this application's data files? Perhaps the window is wide enough for a cold backup, which would make life a lot easier.

If you have a small downtime window but have sufficient disk space, perhaps using the Logical Volume snapshot feature is an option.

## Backup and Restore Tools

There are a variety of methods of performing backups with SLES. They include the general-purpose command-line tools included with every Linux distribution, such as tar, dd, dump, and cpio. Newer Linux distributions, such as SLES 9, include some text-based utilities, such as AMANDA (Advanced Maryland Automatic Network Disk Archiver) and taper. These utilities are designed to add a more user-friendly interface to the backup and restore procedures. GUI-based utilities are available as well, such as the System Backup and Restore modules in YaST. Finally, many commercial backup utilities are also available, such as BRU, CTAR, ARCserve, Legato NetWorker, and System Backup Administrator. Any one of these backup solutions can provide protection for your valuable data.

> **CAUTION**
>
> When you are selecting a backup utility, ensure it supports the filesystem types that you are using. For instance, Legato NetWorker 7.2 for Linux supports ext2/ext3, ReiserFS, and JFS (Journaled File System), but not XFS.

## CHAPTER 10: Data Backup and Disaster Recovery

When deciding on a backup solution, you need to consider the following factors:

- **Portability**—Is backup portability (that is, the ability to back up data from your system server and restore it to another server running a different Linux distribution or implementation of Unix) important to you? For example, can you port the backup from SLES 9 to HP/UX? If so, you’ll probably want to choose one of the standard command-line tools such as `tar`, `dd`, or `cpio`, because you can be reasonably sure that such tools will be available on any Linux/Unix system.
- **Unattended backups**—Is the ability to automate backups so that they can be performed at regular intervals without human intervention important to you? If so, you will need to choose both a tool and a backup medium that support such a backup scheme.
- **Ease of use**—Is a user-friendly interface important to you? If so, you will likely want to choose a tool that provides either a text- or GUI-based interface. Commercial products may provide the easiest interfaces as well as added technical support.
- **Remote backups**—Do you require the ability to start backups and restores from a remote machine? If so, you’ll probably want to choose one of the command-line tools or text-based utilities instead of the GUI-based utilities (unless you have a reasonably fast network connection and the ability to run remote X sessions).
- **Network backups**—Is performing backups and restores to and from networked hosts important to you? If so, you’ll probably want to use one of several of the command-line utilities (such as `tar`) that support network access to backup devices, or a specialized utility such as Amanda or one of the commercial products.
- **Media type support**—Backups can be stored on a variety of media, such as tape, an extra hard drive, ZIP drives, or rewritable DVDs. Consider cost versus reliability, storage capacity, and transfer speed and select a backup application that supports your chosen device type.

> **TIP**
>
> Often, even if your selected tool doesn’t have a built-in scheduler to automate and run backups unattended, you may be able to automate such backups by using cron facilities.

In the following sections, we discuss methods for performing backups and restores using the following tools:

- tar
- dump and restore
- cpio
- dd
- rsync
- AMANDA
- YaST’s System Backup and Restore modules

### Making Tarballs

The tar (tape archive) utility is probably the most commonly used application for data backup on Linux/Unix systems. Why? Because, like vi, you can be guaranteed that any Linux/Unix system will have tar. Furthermore, this tool has been ported to a wide range of hardware platforms and operating systems. Therefore, if you need your backups to be portable across different versions of SUSE, other Linux distributions, to Unix platforms (such as HP/UX or AIX), other operating systems (such as Windows), or even to mainframes, tar would be an excellent choice.

tar was designed to create a tape archive (a large file that contains, or “archives,” other files). In addition to file contents, an archive includes header information to each file inside it. This header data can be used when extracting files from the archive to restore information about the files, such as file permissions, ownerships, and modification dates. An archive file can be saved to disk (and later copied to tape or transferred to another storage medium), written directly to tape, or transmitted across the network while it is being created.

> **NOTE**
>
> The tar archive file is officially referred to as a tarfile. However, it is often (affectionately) called a tarball instead. Frequently, source codes for Linux/Unix-related applications are available as tarballs on the Internet.
>
> By convention, tarfiles use `.tar` as their filename extension. You will also encounter `.tar.gz` or `.tgz` extensions, which identify tar archives that have been compressed using gzip.

Although many command-line options are available with tar, Table 10.5 shows a list of the most commonly used option switches.

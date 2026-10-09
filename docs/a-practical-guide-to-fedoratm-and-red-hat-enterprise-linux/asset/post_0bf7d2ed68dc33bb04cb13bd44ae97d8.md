
## Backing Up Files

One of the most neglected tasks of system administration is making backup copies of files on a regular basis. The backup copies are vital in three instances: when the system malfunctions and files are lost, when a catastrophic disaster (fire, earthquake, and so on) occurs, and when a user or the system administrator deletes or corrupts a file by accident. Even when you set up RAID (page 42), you still need to back up files. Although RAID can provide fault tolerance (helpful in the event of disk failure), it does not help when a catastrophic disaster occurs or when a file is corrupted or removed accidentally. It is a good idea to have a written backup policy and to keep copies of backups offsite (in another building, at home, or at a different facility or campus) in a fireproof vault or safe.

The time to start thinking about backups is when you partition the disk. Refer to “Partitioning a Disk” on page 39. Make sure the capacity of the backup device and your partition sizes are comparable. Although you can back up a partition onto multiple volumes, it is easier not to—and it is much easier to restore data from a single volume.

You must back up filesystems regularly. Backup files are usually kept on magnetic tape, an external hard disk, or other removable media. Alternatively, you can keep backup files on a remote system. How often and which files you back up depend on the system and your needs. Use this criterion when determining a backup schedule: If the system crashes, how much work are you willing to lose? Ideally, you would back up all files on the system every few minutes so you would never lose more than a few minutes of work.

Of course, there is a tradeoff: How often are you willing to back up the files? The backup procedure typically slows the system for users, takes a certain amount of your time, and requires that you have and store the media holding the backup. Avoid backing up an active filesystem; the results might be inconsistent, and restoring from the backup might be impossible. This requirement is a function of the backup program and the filesystem you are backing up.

Another question is when to run the backup. Unless you plan to kick users off and bring the system down to single-user mode (not a user-friendly practice), you will want to perform this task when the machine is at its quietest. Depending on the use of the system, sometime in the middle of the night can work well. Then the backup is least likely to affect users, and the files are not likely to change as they are being read for backup.

A **full** backup makes copies of all files, regardless of when they were created or accessed. An *incremental* backup makes copies of those files that have been created or modified since the last (usually full) backup.

The more people using the system, the more often you should back up the filesystems. One popular schedule is to perform an incremental backup one or two times a day and a full backup one or two times a week.

### Choosing a Backup Medium

If the local system is connected to a network, you can write backups to a drive on another system. This technique is often used with networked computers to avoid the cost of having a backup drive on each computer in the network and to simplify management of backing up many computers in a network. Although tapes are still used for backups, hard disks are being used more frequently. Backing up to a hard disk on a remote system is cost-effective, reliable, and practical. Because hard disks hold terabytes of data, using them simplifies the task of backing up the system, making it more likely that you will take care of this important task regularly. Other options for holding backups are writable CD/DVDs and USB flash drives. These devices, although not as cost-effective or able to store as much information as hard disk or tape systems, offer the benefit of convenience.

### Backup Utilities

A number of utilities are available to help you back up a system, and most work with any media. Most Linux backup utilities are based on one of the archive programs—tar or cpio—and augment these basic programs with bookkeeping support for managing backups conveniently.

You can use any of the tar, cpio, or dump/restore utilities to construct full or partial backups of a system. Each utility constructs a large file that contains, or archives, other files. In addition to file contents, an archive includes header information for each file it holds. This header information can be used when extracting files from the archive to restore file permissions and modification dates. An archive file can be saved to disk, written to tape, or shipped across the network while it is being created.

In addition to helping you back up the system, these programs offer a convenient way to bundle files for distribution to other sites. The tar program is often used for this purpose, and some software packages available on the Internet are bundled as tar archive files.

The amanda (Advanced Maryland Automatic Network Disk Archiver) utility (www.amanda.org), which is one of the more popular backup systems, uses dump or tar and takes advantage of Samba to back up Windows systems. The amanda utility backs up a LAN of heterogeneous hosts to a hard disk or tape. Relevant software packages are amanda-client and amanda-server.

#### tar: Archives Files

The tar (tape archive) utility—see page 249 for an introduction—writes files to and retrieves files from an archive; it can compress this archive to conserve space. If you do not specify an archive device, tar writes to standard output and reads from standard input. With the -f (-file) option, tar uses the argument to -f as the name of the archive device. You can use this option to refer to a device on another system on the network. Although tar has many options, you need only a few in most situations. The following command displays a complete list of options:

```
$ tar --help | less
```

Most options for **tar** can be given either in a short form (a single letter) or as a descriptive word. Descriptive-word options are preceded by two hyphens, as in `--help`. Single-letter options can be combined into a single command-line argument and need not be preceded by a hyphen (for consistency with other utilities, it is good practice to use the hyphen anyway).

Although the following two commands look quite different, they specify the same **tar** options in the same order. The first version combines single-letter options into a single command-line argument; the second version uses descriptive words for the same options:

```bash
# tar -ztvf /dev/st0
# tar --gzip --list --verbose --file /dev/st0
```

Both commands tell **tar** to generate a (**v**, verbose) table of contents (**t**, list) from the tape on `/dev/st0` (f, file), using **gzip** (z, gzip) to decompress the files.

Unlike the original UNIX **tar** utility, when you specify an absolute pathname when you archive a file, the GNU version strips the leading `/` from the file pathname. Also, when it extracts files from a compressed archive, it decompresses them automatically. The first of the following commands shows **tar** compressing (**j** causes **tar** to compress using **bzip2**; page 245) and archiving some files from the `/etc` directory; it displays a message telling you it is stripping the leading /s. The second command extracts the files to the working directory. Because **tar** strips the leading `/` from each pathname, the files are not restored to their original locations in the root directory (/). The third command shows the extracted files in the working directory.

```bash
$ tar -cvjif etc.gtk
tar: Removing leading '/' from member names
/etc/gtk-2.0/
/etc/gtk-2.0/x86_64-redhat-linux-gnu/
/etc/gtk-2.0/x86_64-redhat-linux-gnu/gtk.immodules
/etc/gtk-2.0/gtkrc
/etc/gtk-3.0/
/etc/gtk-3.0/settings.ini

$ tar -xvf etc.gtk
gtk/gtk-2.0/
etc/gtk-2.0/x86_64-redhat-linux-gnu/
etc/gtk-2.0/x86_64-redhat-linux-gnu/gtk.immodules
etc/gtk-2.0/gtkrc
etc/gtk-3.0/
/etc/gtk-3.0/settings.ini

$ ls etc
gtk-2.0     gtk-3.0
```

You can use the `--C` option to cause **tar** to extract files to a directory other than the working directory. The argument to this option specifies the directory **tar** extracts the files to. The options in Table 15-1 tell the **tar** program what to do. You must include exactly one of these options in a **tar** command. The `–c`, `–t`, and `–x` options are used most frequently.


The first time you use a tape, you may receive an error message. Typing `mt fsf 1`, ejecting the tape, and using it again should then work. The `mt` program can be used for various other tape operations, such as setting a tape drive’s built-in compression features. Consult the `mt` man page for details.

The `tar` program compresses data by creating an archive and then compressing it. One consequence of this approach is that if a tape develops a flaw, all data after that flaw will become unusable when you attempt to restore it. For this reason, it’s generally best to not use the `-bzip2` or `--gzip` options when creating tape backups. Tape drives’ built-in compression features are usually more robust to such problems. Hard disk and CD-R media are usually reliable enough that `tar`’s compression isn’t a problem when using these media.

The `--one-file-system` function modifier is important for real-world operation because it prevents `tar` from attempting to back up virtual filesystems, such as `/dev` and `/proc`. These filesystems (especially `/proc`) contain files that FreeBSD generates on the fly and that will needlessly consume disk space. Indeed, attempting to restore such files can conceivably cause problems. If you use the `--one-file-system`, though, you must list each partition you want to back up as a separate file on the `tar` command line. For instance, suppose you’ve got a computer with separate root (`/`), `/tmp`, `/var`, `/usr`, and `/home` partitions. You could back up this system with a command such as

```sh
# tar cvqpf /dev/sa0 /home /var / /usr /tmp
```

This example orders partitions according to the likelihood of a need to recover data from a partition (data stored early is more quickly recovered than data stored late). You might reasonably omit the `/tmp` partition because its data are not guaranteed to survive a reboot.

Ordinarily, `tar` strips the leading slash from absolute filename paths, which can help prevent problems on restore. For instance, you might need to use an emergency system to restore data, mounting your ordinary FreeBSD directory tree in an unusual location, such as `/mnt`. You can then change to `/mnt` and `--extract` to recover your data without overwriting your emergency system’s files. Using `--absolute-paths` tells `tar` to store the leading slash in filenames. You might do this when creating archive files of programs that must reside in specific directories, but even then it’s more common to create a standard relative `tar` file.

If you download a tarball, don’t extract it without first examining its contents with `--list`. A malicious or ignorant individual could create a tarball with absolute paths and load it with files that would overwrite your ordinary system utilities, thus creating a security breach or making your system unusable.

## Restoring Data

A backup is only as useful as your ability to restore data from it. In the case of `tar` and `cpio`, restoring data involves the same utilities, and basically the same commands, as backing it up. This restoration process is simplest when your system works and you just need to restore a few files. For instance, suppose the `walter` user comes to you and says he accidentally deleted a file from his home directory. If `walter` remembers that the file's name is `report78.tex`, you might issue commands such as the following to recover the file:

```sh
# cd /
# tar xvfp /dev/sa0 home/walter/report78.tex
```

**Note**: Because `tar` normally stores files without the leading slash, you must change to the root directory, or to the directory from which a backup was made, and give the name of the file to be restored without its leading slash, to successfully restore a file.

If `walter` doesn't remember the exact name of the file, you may need to use `tar`'s `--list` function to locate the file before restoring it. You could also restore an entire directory tree by listing the directory tree's name. If you don't provide a file name when restoring data, `tar` attempts to restore the entire contents of the backup, which is more than you need in most cases.

**Tip**: You can practice making backups using a spare directory. Copy some files to this directory, then restore them to another directory and check that they were restored correctly.

In extreme emergencies, you may need to recover an entire FreeBSD system or files that are needed for basic operation. For instance, your hard drive might have failed, or somebody might have broken into your system and compromised its security. In such situations, a full restore is necessary. You can approach this problem in several ways:

- **Emergency systems**: You can use a FreeBSD emergency boot system, as described in Chapter 32, to boot FreeBSD, prepare new partitions, and restore all your data. This approach takes careful planning *before* disaster strikes.
- **Partial normal install**: You can install a minimal FreeBSD system and use it as if it were an emergency system. For instance, you might install FreeBSD on an old hard disk and use that to restore your regular system to a larger disk, and then reconfigure your disks so that the larger disk is the normal boot disk.
- **Full install and modification**: You can reinstall FreeBSD in the normal way, and then use your backup to restore only key directories that are likely to have changed, such as `/home`. This approach becomes more difficult the more your system diverges from a standard FreeBSD installation; even with complete notes on your customizations, it can take hours to restore a system to its former normal operating condition.

Emergency full restores can be a nightmare, and that nightmare is all the worse when you're unprepared. For this reason, you should consider what you would do if your hard disk were to stop working or if some other disaster struck. How would you recover your data? If you don't know, you should think the matter through and come up with a recovery plan. If at all possible, you should practice your restoration plan. For instance, you might try recovering a system to a spare computer and try booting that computer. (Hardware differences could cause problems even if the process works, though.) The more critical your FreeBSD system is to yourself or your business, the more time you should invest in preparing for problems.

## Summary

Various metadata are associated with FreeBSD files. These include the file's owner, group, and permissions, and this information is critical for using certain file manipulation commands. You can't copy a file if you can't read it, for instance, and you must be able to write to a directory to copy or move a file into that directory. FreeBSD relies upon a handful of file manipulation commands to modify metadata, move files, copy files, delete files, find files, and so on. A good grasp of these commands will help you immensely in both using and administering a FreeBSD system. Managing files also involves protecting them from disaster by backing them up to external media such as CD-Rs or tapes. Thereafter, in the event of a major or minor disaster, you can recover your data quickly.

# Chapter 9

# Printer Configuration

![](img/f34d37e3abe9f4517128e54f80ab2616_274_0.png)

The paperless office has long been an enticing dream. It has remained just that— a dream—for quite a while, though, and will likely remain so for some time to come. For this reason, printing is an important task for FreeBSD. If you're used to printing in Windows, OS/2, Mac OS, or a similar OS, you may find the FreeBSD printing model odd. Although FreeBSD's printing system bears some similarity to those of other systems, there are also very important differences. Thus, this chapter begins with a look at FreeBSD printing theory. It moves on to the practical tasks of creating a print queue, setting up Ghostscript (which functions as a printer driver), controlling an existing print queue, and controlling network access to the printer.

## Understanding the FreeBSD Printing Model

Most modern OSs use a *print queue*, which is a holding area for documents that should be printed. In FreeBSD, various programs exist to submit documents to the print queue; prioritize and otherwise manipulate *print jobs*, as the documents are called once in the queue; process print jobs into a form that a printer can understand; and send print jobs to printers. Understanding how various FreeBSD printing tools fit into this model will help you to configure your print queue when it comes time to dig into the actual configuration files.

## The Need for Print Queues

If you remember the days of DOS, you may recall how printers worked in that OS: Programs sent data directly to the printer port hardware. DOS itself did little to control access to the printer, and programs were responsible for delivering data in a format that the printer could understand. With the advent of multitasking OSs, though, a more sophisticated model became necessary. In an OS such as FreeBSD, programs can't be trusted to send data directly to the printer port. Imagine two programs attempting to send data at once. At best, one program would be denied access to the hardware, and the print job would fail. Multiple users could end up fighting each other for access to the printer, each trying to submit a print job in the brief interval between competing print jobs. At worst, both programs could write data, resulting in output that's a mixture of two jobs or complete gibberish.

Print queues solve this problem by enabling the OS to both accept multiple print jobs and schedule them to be sent to the printer in succession. While FreeBSD sends one job to the printer, the second is stored on disk in an area known as a *print spool* (in a subdirectory of `/var/spool/lpd`, typically). Because the OS controls the process, it can accept an arbitrary number of print jobs and queue them up for the printer. In practice, of course, the number of jobs is limited by the available disk space in the `/var` partition or whatever partition houses `/var/spool/lpd`.

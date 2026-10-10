
You can create a schedule in which you do a full backup of the entire computer only occasionally—say, once a week or once a month. You’d do this by deleting the increment file and running a backup as usual. On intervening weeks or days, you can perform an incremental backup, thus saving time.

With cpio, the key to incremental backups is in the list of files fed to the program. You can perform an incremental backup by using find options to locate only new files or files that have changed since the last backup. For instance, the `-newer file` option to `find` causes that program to return only files that have been modified more recently than `file`. Thus, you could create a file (perhaps a log of your backup activity) during each backup and use it as a way of determining what files have been modified since the last backup.

Performing incremental backups has a couple of drawbacks. One is that they complicate restoration. Suppose you do a full backup on Monday and incremental backups every other day. If a system fails on Friday, you’ll need to restore the full backup and several incremental backups. Second, after restoring an incremental backup, your system will contain files that you had deleted since the full backup. If files have short life spans on a computer, this can result in a lot of “dead” files being restored when the time comes to do so.

Despite these problems, incremental backups can be extremely useful for helping make backups manageable. They can also reduce wear and tear on tapes and tape drives, and they can minimize the time it takes to restore files if you know that the files you need to restore were backed up on an incremental tape.

## Preparing for Disaster: Backup Recovery

Creating backups is advisable, but doing this isn’t enough. You must also have some way to restore backups in case of disaster. This task involves two aspects: partial restores and emergency recovery.

Partial restores involve recovering just a few noncritical files. For instance, users might come to you and ask you to restore files from their home directories. You can do so fairly easily by using the `--extract` (`x`) tar command:

```bash
# cd /
# tar xvfp /dev/st0 home/username/filename
```

> **Note**: This sequence involves changing to the root directory and issuing a relative path to the file or directory that must be restored. This is required because tar normally strips away the leading `/` in files it backs up, so the files are recorded in the archive as relative filenames. If you try to restore a file with an absolute filename, it won’t work.

When you’re using cpio, the procedure is similar, but you use the `--extract` (`-i`) option, along with other options to feed the name of the archive, and perhaps do other things:

```bash
# cd /
# cpio -iVf /dev/st0 home/username/filename
```

Whether you're using tar or cpio, you'll need to know the exact name of the file or directory you want to restore in order to do this. If you don't know the exact filename, you may need to use the `--list` (`t`) command to cpio or tar to examine the entire contents of the tape, or at least everything until you see the file you want to restore.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_375_0.png)

> If you use incremental backups, you can use the incremental file list to locate the filename you want to restore.

A much more serious problem is that of recovering a system that's badly damaged. If your hard disk has crashed or your system has been invaded by crackers, you must restore the entire system from scratch, without the benefit of your normal installation. In most cases, an emergency system, as described in Chapter 1, will do the job. You'll need to ensure beforehand that your emergency system has the tools you need to access your backups.

Whatever approach you choose to use, you should test it before you need it. Learn at least the basics of the tools available in any system you plan to use. If you use unusual backup tools (such as commercial backup software), be sure to copy those tools to your emergency system or have them available on a separate removable disk. If you'll need to recover clients via network links, test those setups as well.

You may not be able to completely test your emergency restore tools. Ideally, you should boot the tools, restore a system, and test that the system works. This may be possible if you have spare hardware on which to experiment, but if you lack this luxury, you may have to make do with performing a test restore of a few files and testing an emergency boot procedure. Note that a freshly restored system will not be bootable; you'll need a way to restore your boot loader from an emergency boot.

## Writing to Optical Discs

Optical media are an extremely popular means of exchanging moderately large files. Most CD-R and CD-RW media hold 700MB of files (older discs held 650MB), recordable DVD formats have capacities of 4.7~8.5GB, and Blu-ray discs hold 25~50GB. Plain write-once CDs and DVDs cost $0.10 to $1 and are likely to remain readable for several years to decades, given proper storage. You can't simply mount an optical disc and write files to it as you would a floppy disk, though; you must create a complete filesystem and then copy (or "burn") that filesystem to the disc. This process requires using two tools, `mkisofs` and `cdrecord`, or requires variants of or front-ends to these tools.

### Linux Optical Disc Tools

The Linux optical disc creation process involves three steps:

- 1. Collect source files. You must first collect source files in one location, typically a single subdirectory of your home directory.
- 2. Create a filesystem. You point a filesystem-creation program, `mkisofs`, at your source directory. This program generates an ISO-9660 filesystem in an image file. Alternatively, you can create another filesystem in an appropriately sized partition or image file and copy files to that partition or image file. This latter approach can be used to create ext2fs, FAT, or other types of optical discs, but there’s seldom any advantage to doing this.
  > If you install an OS to a partition that’s less than your media’s size, you can back it up by burning the partition directly to CD-R or recordable DVD. The result is a disc that uses the OS’s native filesystem. You can restore the backup by using `dd`, assuming the target partition is exactly the same size as the original.
- 3. Burn the disc. You use an optical disc-burning program, such as `cdrecord`, to copy the image file to the optical device.
  > Recent Linux distributions provide both `mkisofs` and `cdrecord` in a single package called `cdrttools`.

The `growisofs` program combines the functionality of `mkisofs` and `cdrecord`, but `growisofs` works only with DVDs and Blu-ray discs, not with the smaller CD-Rs. In turn, many versions of `cdrecord` won’t work with the larger DVDs and Blu-ray discs! Another approach to optical disc creation is to use GUI front-ends to the text-mode tools. These GUI tools provide a point-and-click interface, eliminating the need to remember obscure command-line parameters. Popular GUI Linux optical disc creation tools include X-CD-Roast (http://www.xcdroast.org), GNOME Toaster (http://gnometoaster.rulez.org), and K3B (http://k3b.sourceforge.net).

All of these optical disc tools provide a dizzying array of options. For the most part, the default options work quite well, although you will need to provide information to identify your drive and burn speed, as described in the next section. Some `mkisofs` options can also be important in generating image files that can be read on a wide variety of OSs, as described later in “Creating Cross-Platform Discs.”

### A Linux Optical Disc Example

To begin creating optical discs, starting with `mkisofs` makes sense:

```bash
$ mkisofs -J -r -V "volume name" -o ../image.iso . /
```

This command creates an image file called `image.iso` in the parent of the current directory, placing files from the current working directory (.) in the resultant image file. The `-J` and `-r` options enable Joliet and Rock Ridge extensions, respectively, and the `-V` option sets the volume name to whatever you specify. Dozens of other options and variants on these are available; check the `mkisofs` man page for details.

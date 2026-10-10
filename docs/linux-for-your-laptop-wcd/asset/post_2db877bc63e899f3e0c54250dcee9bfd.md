
- Friday: Backup of all changed files since Thursday
- Saturday: Backup of all changed files since Friday

This strategy has the advantage in that you could lose only several hours' work; however, restoring a full backup and maintaining this schedule would require seven sets of media! Fortunately, most experienced mobile Linux users know that only one, or maybe two, directories are truly critical to a typical Linux installation:

- *etc/. The all-important configuration files directory
- *home/. Users, FTP, and http's directories

The *etc* directory typically consists of 3 to 4MB of configuration files, scripts, and other items. On the other hand, the *home* directory, especially on systems supporting multiple users, can grow into the gigabyte range! Even a mobile Linux user's *home* directory can grow to several hundred megabytes, depending on documents, installed software, and e-mail directories and folders.

You'll need to decide how often and what type of backup strategy to use for your notebook. You'll then need to choose a backup *medium* or type of storage to use for your backups.

## Backup Devices

Choosing an appropriate backup medium or device is a matter of cost, speed, capacity, reliability, and appropriateness. For example, you don't need a 20GB tape drive if you need to back up only 100MB of files (unless you want to keep all your backups on a single tape, which isn't a good idea). If you have to back up only several megabytes of files, you can get away with using floppy diskettes, but you should make extra copies just in case a floppy becomes corrupted.

If you use Linux in a business environment, choose your backup device carefully. These devices range from high-speed digital tapes requiring SCSI interfaces to optical CDRW disks. Mobile Linux users who need large data backups should consider testing any external units before committing to a particular device. Remember that a notebook's 16-bit *PCMIA* interface limits backups to about 3MB per second. With the advent of newer Linux kernels and improved CardBus services, expect higher backup speeds, along with better support for higher-speed USB or even Firewire devices. For all practical purposes, however, cost-conscious mobile Linux users will choose a less-expensive route to data backup.

## Swap Your Hard Drive?

If you have one of the higher-end notebooks from IBM, Compaq, or Dell, and you need to quickly exchange data, consider purchasing an extra hard drive that you can swap out of your notebook. Some items are expensive but are worth it if you end up having problems. These notebooks allow you to have two hard drives active at the same time, so you can quickly back up data from one drive to another. If you have only one drive bay, you can keep a fully configured Linux filesystem on the extra drive as a quick replacement should your main drive expire.

One popular device that provides relatively inexpensive but reliable storage is the Iomega Zip drive. See the section “Using Iomega Zip Drives” in Chapter 12, “Data Synchronization,” for details on installing a parallel-port Zip drive. After it’s installed, you can use nearly any type of commercial or Open Linux backup software with this drive.

## Backup Software

The cp, dump, cpio, tar, and related commands comprise the generic Linux backup software included with every Linux distribution. If you want to devise automated backups, you need to write shell scripts and use the cron daemon to run these backups on schedule. To create a regularly scheduled backup for your notebook, one approach might be to combine the output of the `find` command, along with `tar` or `cpio`, and target and back up a specific directory.

For example, the `find` command’s -mtime option, followed by an integer (in days), returns a list of files that have been modified in the last 24 hours. You can then feed, or `pipe`, this information to the `cpio` command to create an incremental backup of the previous day’s files:

```bash
# /usr/bin/find /home -mtime 1 -print | /bin/cpio -o > /mnt/backup/Monday.cpio
```

This command line could be placed in a shell script named monday_backup (and perhaps saved in root’s bin directory) and then put into your Red Hat, Mandrake, or Yellow Dog Linux `/etc/crontab` file like this:

```text
30 2 * * 1 root /root/bin/monday_backup
```

This creates the backup file Monday.cpio every Monday morning at 2:30 a.m. You can use many different approaches to automate your backups, and you have a variety of ways in which to use your Linux filesystem tools.

## Finding the rhbackup Script

Red Hat Linux, until version 5.2, included a useful shell script named rhbackup that could be used to perform backups locally or over a network. You can still find a copy at

http://rpmfind.net/linux/RPM/redhat/5.2/i386/rhbackup-0.2-1.noarch.html

**Mobile Linux iBook users can find a copy at**

http://rpmfind.net/linux/RPM/yellowdog/1.0/old_releases/champion-1.1/ppc/RedHat/RPMS/rhbackup-0.2-2.noarch.html

A number of commercial backup software packages are also available for Linux. One popular package, BRU (backup and restore utility), by Enhanced Software Technologies, features a complex command-line or easy-to-use graphical interface for backing up your system’s software. You might find BRU packaged in a *personal edition* as value-added software included with various Linux distributions. However, you can also download a 30-day demonstration version from http://www.estinc.com.

BRU should be run as root, and you must run X11 in order to use BRU’s graphical interface. Install the software using the *rpm* command, and then type the command *xbru &* from the command line of an X11 terminal to start the program. You’ll see the startup dialog box, shown in Figure 13.1.

When the program first starts, you must configure BRU to use your backup device. This device can be one of many predefined tape drives, a floppy disk, or, if you need it, a custom-configured device you define for your system. Choose File, Configure Bru. In the configuration dialog box that appears, click the Devices tab, and then click the New button. You’ll see the dialog box shown in Figure 13.2. This dialog box lists more than two dozen different devices. If you scroll down to the end of the list, you’ll see an OTHER entry. You can use this entry to define your own device. For now, just select the 1.44Mb Floppy entry.

Click the Create button, choose File, Save, and then exit the configuration dialog box. You’ll return to the main BRU window (shown in Figure 13.1). To select

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_328_0.png)

Figure 19.1 The BRU backup utility features a graphic interface for performing system backups.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_328_1.png)

Figure 19.2 The BRU backup utility can use predefined or custom-configured backup devices.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_329_0.png)

directories and files to be backed up, click the topmost button along the left side of BRU's main window (the Backup Data to Archive button). You'll see the file selection dialog box shown in Figure 13.3.

When you've finished selecting files and directories, click the Start Backup button to begin your backup. You'll be prompted to insert and remove floppy diskettes. Don't forget to properly label your diskettes during the backup! After that, you can use BRU's buttons on its main dialog box to restore, list, or verify your archive.

## Alternative Backup Methods

If you don't want to carry a bulky backup device with you on the road, and you have only a few files to worry about, consider using printouts, or save your files on floppy disks. If you have 64MB or less of data to back up, consider using a flash memory card. These devices are relatively inexpensive when purchased in capacities of 64MB or less and have additional benefits:

- Very lightweight.
- High-density storage in a credit card-sized format.
- Require no external power source.

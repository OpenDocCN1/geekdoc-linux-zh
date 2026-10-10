
Because core files in Fedora and RHEL consist of the word core, followed by a dot (.) and process ID, this example will match all files beginning with core. and followed by a number. The root user can access any user’s individual crontab file by using the `-u username` option to the `crontab` command.

## Understanding cron files

Separate cron directories are set up to contain cron jobs that run hourly, daily, weekly, and monthly. These cron jobs are all set up to run from the `/etc/crontab` file. The default `/etc/crontab` file looks like this:

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

The first four lines initialize the run-time environment for all subsequent jobs (the subshell in which jobs run, the executable program search path, the recipient of output and error messages, and that user’s home directory). The next five lines execute (as the user root) the run-parts program that controls programs that you may want to run periodically.

run-parts is a shell script that takes a directory as a command-line argument. It then sequentially runs every program within that directory (shell scripts are most common, but binary executables and links are also evaluated). The default configuration executes programs in `/etc/cron.hourly` at one minute after every hour of every day; `/etc/cron.daily` at 4:02 a.m. every day; `/etc/cron.weekly` at 4:22 a.m. on Sundays; and `/etc/cron.monthly` at 4:42 a.m. on the first day of each month.

Here are examples of files that are installed in cron directories for different software packages:

- `/etc/cron.daily/logrotate.cron` — Automates rotating, compressing, and manipulating system logfiles.
- `/etc/cron.daily/makewhatis.cron` — Updates the whatis database (contains descriptions of man pages), which is used by the man, -k, apropos, and whatis commands to find man pages related to a particular word.
- `/etc/cron.daily/slocate.cron` — Updates the `/var/lib/slocate/slocate.db` database (using the `updatedb` command), which contains a searchable list of files on the machine.
- `/etc/cron.daily/tmpwatch` — Removes files from `/tmp`, `/var/tmp`, and `/var/catman` that haven't been accessed in ten days.

The `makewhatis.cron` script installed in `/etc/cron.weekly` is similar to the one in `/etc/cron.daily`, but it completely rebuilds the `whatis` database, rather than just updating the existing database.

Finally, in the `/etc/cron.d` directory are files that have the same format as `/etc/crontab` files.

> **NOTE:** If you are not comfortable working with `cron` from the command line, there is a KCron Task Scheduler window that comes in the kdeadmin package for managing cron tasks. To launch KCron, type `kcron` from a Terminal window.

## Summary

Shell scripts are an integral part of a Fedora or RHEL system for configuring, booting, administering, and customizing Fedora or RHEL. They are used to eliminate typing repetitive commands. They are frequently executed from the scheduling facilities within Fedora or RHEL, allowing much flexibility in determining when and how often a process should run. They also control the startup of most daemons and server processes at boot time.

The `init` daemon and its configuration file, `/etc/inittab`, also factor heavily in the initial startup of your Fedora or RHEL system. They implement the concept of run levels that is carried out by the shell scripts in `/etc/rc.d/init.d`, and they provide a means by which the machine can be shut down or rebooted in an orderly manner.

To have shell scripts configured to run on an ongoing basis, you can use the `cron` facility. Cron jobs can be added by editing `cron` files directly or by running commands such as `at` and `batch` to enter the commands to be run.

# Chapter 13

## Backing Up and Restoring Files

### In This Chapter

- Doing a simple backup
- Selecting a backup strategy
- Selecting a backup medium
- Backing up to a hard drive
- Backing up files with `dump`
- Automating backup with `cron`
- Restoring backed-up files
- Backing up over the network with Amanda
- Performing network backups with multiple computers
- Using the `pax` archiving utility

If you've ever suffered a hard drive crash, you know just how aggravating it can be. You can lose irreplaceable data. You likely spend countless hours reinstalling your operating system and applications. It is not a fun experience. It need happen only once for you to learn the importance of making regular backups of your critical data.

Today, larger and faster backup media can simplify the process of backing up your data. Fedora and RHEL support many different types of media — such as writable CD (CD-R and CD-RW), DVD (DVD-R, DVD+R, DVD+RW, and DVD-RW), and magnetic tape — for creating backups. Using tools such as `cron`, you can configure backups to run unattended at scheduled times.

This chapter describes how to create a backup strategy and how to select media for backing up data on your Fedora or RHEL system. It tells you how to do automated backups and backups over a network. It also describes how to restore individual files, or entire file systems, using tools such as the `restore` command.

## Making a Simple Backup Archive

Improvements in the GNOME desktop for handling removable media (CDs, DVDs, USB flash drives and so on) can help you to do a quick backup of your personal data. With the GNOME desktop running on your Fedora system, use the following procedure to back up all the data in your home directory:

1. Insert a blank CD or DVD into your computer's drive. An icon appears on the desktop, indicating that a blank disc is ready to be used.
2. Double-click the Blank Disc icon to see the CD/DVD Creator window.
3. Open the folder icon representing your home directory (such as Joe's Home) on the desktop and browse to the /home folder.
4. Drag-and-drop your home directory from the /home folder on to the CD/DVD Creator window.
5. Add other files and folders you want to back up to the CD/DVD Creator window in the same way.
6. When all the files and folders you want to back up are copied to the CD/DVD Creator window, click Write to Disc and the Write to Disc pop-up window appears.
7. Type a disc name for the backup medium and optionally choose the write speed. (The disc name will be used as the name of the mount point if you later open the CD/DVD on the GNOME desktop). Figure 13-1 shows the Write to Disc pop-up and the CD/DVD Creator window (with the home folder of the user joe dragged into that folder).

![](img/fb202c163797a743c3c6cf236316bc96_575_0.png)

8. **Figure 13-1:** Drag-and-drop files and folders on the CD/DVD Creator window for a simple backup. Click *Write* to have the files and folders written to the disc.

This procedure results in a standard *ISO9660* image (with Rock Ridge extensions) being burned to the CD or DVD. That disc can be read from Linux, Windows, or other systems that support that ISO standard. While the procedure is a quick way to save your critical files, you should consider using other backup tools described in this chapter for more flexible and powerful backup methods.

## Doing a Simple Backup with rsync

Cheap hard disk space, fast networks, and some really neat new tools have given Linux users some nice backup alternatives to the old reliable removable media (such as tapes and CD s). To back up your personal data or the data from a small office computer, the examples in this section provide fairly simple ways of creating usable backups of your data.

To do this procedure, you need to have hard disk space on a computer that is at least slightly larger than the hard disk you are backing up. That hard disk space could be on:

- **A different partition** — By backing up to a separate disk partition, you are protected in case the partition you are backing up becomes corrupted. However, you are not protected if your hard disk goes bad.
- **A different hard disk** — Backing up to a separate hard disk can protect from a corrupted disk, but won't help you if your computer is hit by lightning, a flood, or other acts of God.
- **A different computer** — By backing up over the network, you can back up to another computer that is as far away from the source of your data as makes you feel comfortable. You can back up to the computer down the hall or one across the country.

To do the actual backup, you use the rsync command. The rsync command is like a remote copy command (similar to rcp on steroids. In essence, rsync lets you copy files from one location to another. However, it also has some nice extra features that enable you to do the following:

- **Transfer differences only** — If you transfer a file that was transferred during an earlier backup, rsync uses a checksum-search algorithm to determine the differences between the old file and the new one. Then it sends only the data needed to account for the differences between the two files.
- **Transfer data securely** — rsync combines with ssh (or another remote shell) to encrypt the data, so it can travel securely across a network.
- **Maintain ownership** — The transferred files can keep their some permissions, ownership, timestamps, and group designations. (Because ownership is based on numeric UID and GID, matching user and group accounts must be set up between machines for the files to appear to be owned by the same users and groups after the files are copied.)

The following sections show examples of the rsync command at work.

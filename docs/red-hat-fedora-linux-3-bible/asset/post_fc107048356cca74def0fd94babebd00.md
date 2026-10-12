
# Chapter 13: Backing Up and Restoring Files

> **NOTE:** Notice that there's no trailing slash after `/home/chris` (so it's not `/home/chris/`). Without that trailing slash, `rsync` will copy files from that directory to a target directory named `chris` (`/mnt/backup/homes/chris`). With a trailing slash, all files from `/home/chris/` are copied directly to the homes directory (`/mnt/backup/homes/`).

In this example, the entire contents of the `/home/chris` directory structure are added to the `/mnt/backup/homes/chris` directory. All files, subdirectories, links, devices and other file types are copied. By using the archive option (-a), all ownership, permissions, and creation times are maintained on the copied files.

If `/mnt/backup/homes` is on a separate disk, you now have your entire `/home/chris` directory copied in two places on the same machine. If the `/mnt/backup/homes` directory is an NFS shared directory (with write permission on), the files are now backed up to another machine.

Since the example is a backup of my personal files that don't change too often, after a few days of changes to the files, I might want to run the exact same command again:

```bash
# rsync -av /home/chris /mnt/backup/homes/
```

This time any new files are copied to the target directory and the changes to any files I modified are applied to the original backup files. Any files I deleted from my home directory will still be in the target directory (`rsync` doesn't remove deleted files unless you specifically tell it to). The result is, again, a complete copy of the `/home/chris` directory at the moment the `rsync` command is run, plus any files that have been deleted from any `/home/chris` directories.

> **NOTE:** If you want files that were deleted from the sending directory to be likewise deleted from the target directory, you can add the `-delete` option to `rsync`.

## Backing up files remotely

While the previous example was a quick, informal backup method, with more critical data, you want to make sure that the data are being backed up to another computer and that the backup is done at regular intervals. This can be accomplished by using `rsync` in concert with `ssh` and `cron`.

Having `ssh` as the transport mechanism ensures that data will be encrypted when it is transferred. Also, because the `ssh` service (`sshd`) is enabled by default on many Fedora and Red Hat Linux systems, you need only a user name and password to the remote system to do the backup. (As long as you can use `ssh` to connect to the remote machine and `rsync` is installed remotely, you can use the `rsync` command to transfer files there.) Here's an example:

```bash
# rsync -avz -e ssh /home/chris duck:/mnt/backup/homes/
root@duck's password: ********
building file list ... done
```

Here, I identify the remote computer (named `duck` in this case) by putting it before the remote directory name, separated with a colon. I use some different options as well. To the archive (`-a`) and verbose (`-v`) options, I add the `-z` option to compress the data (making it more efficient to transfer). I also use the `-e ssh` option to have `rsync` use an ssh remote shell to transfer data. The password prompt you see is the ssh login prompt.

You can repeat this command each time you want to back up your files. However, the more efficient way to do this is to set up this command to run as a cron job so that the backups happen automatically at set intervals.

To have `rsync` run automatically, you can’t have it prompt you for a password. To have the `rsync` command run without prompting for a password, follow this procedure:

1. Set up ssh to do no-password logins for the user who is going to perform the backup (see the section “Using ssh, scp and sftp without passwords” in Chapter 14 for information on how to do this).
2. Decide how often you want the backup to run. For example, if you want to run the `rsync` command once each day, as root user you could create a file called `/etc/cron.daily/mybackup`.
3. Set permissions to be executable:
   ```bash
   # chmod 755 /etc/cron.daily/mybackup
   ```
4. Add the command line to the mybackup file that you want to use:
   ```bash
   rsync -azv -e ssh /home/chris chris@duck:/mnt/backup/names/
   ```

Notice that I added the user name `chris` as the log-in user name on the remote computer (`duck`). For you, this will be the name of the person for which you set up a no-password login in step 1.

At this point, a backup will be done once each day to the machine specified.

> **NOTE:** With the simple backup command just shown, you can build on more complex features. In particular, you might want to think about building in a snapshot feature. Snapshots allow you to go back to a particular date and time to restore a backed-up file. Mike Rubel has an excellent procedure for doing `rsync` snapshots at his home, `mikerubel.org/computers/rsync_snapshots`, entitled “Easy Automated Snapshot-Style Backups with Linux and Rsync.”

## Selecting a Backup Strategy

While it is tempting to do the quick-and-easy backup, backing up important data requires more planning and forethought. There are several approaches you can take to backing up your data. You need to ask yourself a few questions to decide which approach is best for you. Some things that you should consider are:

- In the event of a crash, how much downtime can I tolerate?
- Will I need to recover older versions of my files or is the most recent revision sufficient?
- Do I need to back up files for just one computer or for many computers on a network?

Your answers to these questions will help you decide how often to do full backups and how often to do incremental backups. If the data is particularly critical, you may even decide that you need to have your data duplicated constantly, using a technique called disk mirroring. The following sections describe different backup methods.

## Full backup

A full backup is one that stores every file on a particular disk or partition. If that disk should ever crash, you can rebuild your system by restoring the entire backup to a new disk. Whatever backup strategy you decide on, some sort of full backup should be part of it. You may perform full backups every night or perhaps only once every week; it depends on how often you add or modify files on your system, as well as the capacity of your backup equipment.

## Incremental backup

An incremental backup is one that contains only those files that have been added or modified since the last time a more complete backup was performed. You may choose to do incremental backups to conserve your backup media. Incremental backups also take less time to complete, because they only backup data that has changed since the most recent backup (full or incremental). Incremental and other partial backup types can be important when systems are in high use during the work week and running a full backup would degrade system performance. Full backups can be reserved for the weekend when the system is not in use.

## Disk mirroring

Full and incremental backups can take time to restore, and sometimes you just can’t afford that downtime. By duplicating your operating system and data on an additional hard drive, you can greatly increase the speed with which you can recover from a server crash.

With disk mirroring, it is usually common for the system to continuously update the duplicate drive with the most current information. In fact, with a type of mirroring called RAID 1 (described in Chapter 10), the duplicate drive is written to at the same time as the original, and if the main drive fails, the duplicate can immediately take over. This is called fault-tolerant behavior, which is a must if you are running a mission-critical server of some kind.

## Network backup

All of the preceding backup strategies can be performed over a network. This is good because you can share a single backup device with many computers on a network. This is much cheaper and more convenient than installing a tape drive or other backup device in every system on your network. If you have many computers, however, your backup device will

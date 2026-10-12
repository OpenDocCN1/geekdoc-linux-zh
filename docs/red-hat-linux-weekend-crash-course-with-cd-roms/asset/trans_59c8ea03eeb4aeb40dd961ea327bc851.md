
Typically, you have to follow a strict regimen of regular backups because you can never tell when the hard disk might fail or the file system might get corrupted. To implement such a regimen, you need to decide what files to back up, how often to back them up, and what backup storage media to use. This involves selecting a backup strategy and backup media.

Your choice of backup strategy and backup media depend on your assessment of the risk of business disruption due to hard disk failure. Depending on how you use your Red Hat Linux system, a disk failure may or may not have much impact on you.

For example, if you use your Red Hat Linux system as a learning tool (to learn about Linux or programming), all you may need are backup copies of some system files needed to configure Red Hat Linux. In this case, your backup strategy may be to save important system configuration files on one or more floppies every time you change any system configuration.

On the other hand, if you use your Red Hat Linux system as an office server that provides shared file storage for many users, the risk of business disruption due to disk failure is much higher. In this case, you have to back up all the files every week and back up any new or changed files every day. You should perform these backups in an automated manner (using the job-scheduling features that you learned in Session 25). Also, you probably need a backup storage medium that can store large amounts (multiple gigabytes) of data on a single tape. In other words, for high-risk situations, your backup strategy is more elaborate and thus requires additional equipment such as a tape drive.

Your choice of backup media depends on the amount of data you have to back up. For a small amount of data, such as system configuration files, you can use floppy disks as your backup media. If your PC has a Zip drive, you can use Zip disks as your backup media. (These are good for backing up a single user directory.) To back up servers, you should use a tape drive — typically a 4mm or 8mm tape drive that connects to a SCSI controller. Such tape drives can store several gigabytes of data per tape, and you can use them to back up an entire file system on a single tape.

When backing up files to these backup storage media, you have to refer to the backup device by name. Here are the device names for some common backup devices:

| Backup Device | Linux Device Name |
|---|---|
| Floppy disk | /dev/fd0 |
| IDE Zip drive | /dev/hdc4 or /dev/hdd4 |
| SCSI Zip drive | /dev/sda (assuming it’s the first SCSI drive); otherwise, the device name depends on the SCSI ID |
| SCSI tape drive | /dev/st0 or /dev/nst0 (the n prefix means that the tape does not rewind after files are copied to the tape) |

Although this session focuses on backing up and restoring files with the tape archiver (tar) program that comes with Red Hat Linux, there are other commercially available utilities for Red Hat Linux that perform backups. I highlight some well-known commercial utilities in the following sidebar.

## Backing Up and Restoring Files with the Tape Archiver — tar — Program

You can use the tape archiver program (tar command) to archive files to a device such as a floppy disk or tape. The tar program creates an archive file that can contain other directories and files, and (optionally) compress the archive for efficient storage. The archive is then written to a specified device or another file. In fact, many software packages are distributed in the form of a compressed tar file.

## Commercial Backup Utilities for Red Hat Linux

Although you can manage backups with tar, a number of commercial backup utilities come with graphical user interfaces and other features to simplify backups. Here are some well-known backup utilities for Red Hat Linux:

- **BRU**: Backup and Restore Utility from EST (see http://www.estinc.com/)
- **LONE-TAR**: tape backup software package from Lone Star Software Corporation (see http://www.cactus.com/)
- **Arkeia**: backup and recovery software for heterogeneous networks from Knox Software (see http://www.knox-software.com/)
- **CTAR**: backup and recovery software for UNIX systems from UniTrends Software Corporation (see http://www.unitrends.com/)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_322_0.png)

The command syntax of the tar program is as follows:

```
tar options destination source
```

The options are usually specified by a sequence of single letters, each specifying what tar should do. The device name of the backup device is destination, and source is a list of file or directory names denoting the files to back up.

## Backing up and restoring a single volume archive

Suppose you want to back up the contents of the /etc/X11 directory on a single floppy disk. Log in as root, place a disk in the floppy drive, and then type the following command:

```
tar zcvf /dev/fd0 /etc/X11
```

The tar program displays a list of filenames as each file is copied to the compressed tar archive on the floppy disk. In this case, the options are zcvf, the destination is /dev/fd0 (the floppy disk), and the source is the /etc/X11 directory (which implies all its subdirectories and their contents). You can use a similar tar command to back up files to a tape. Simply replace /dev/fd0 with the tape device — such as /dev/st0 for a SCSI tape drive.

A few common tar options are defined here:

| Option | Definition |
|---|---|
| z | compresses the tar archive using gzip |
| c | creates a new archive |
| v | displays verbose messages |
| x | extracts files from the archive |
| t | lists the contents of the archive |
| M | specifies a multi-volume archive (next section describes multi-volume archives) |
| f | specifies the name of the archive file or device on the next field in the command line |

To view the contents of the tar archive you create on the floppy disk, type the following command:

```
tar ztf /dev/fd0
```

You should see a list of the filenames (each begins with /etc/X11) indicating the contents of the backup. In this tar command, the t option lists the contents of the tar archive.

To learn how to extract the files from a tar backup, try the following steps while logged in as root:

- 1. Change the directory to /tmp by typing the command:
  ```
  cd /tmp
  ```
  That is where you extract the files from the tar backup.
- 2. Type the following command:
  ```
  tar zxvf /dev/fd0
  ```
  This tar command uses the x option to extract the files from the archive stored on /dev/fd0 (the floppy disk).

If you check the contents of the /tmp directory, you notice that the tar command creates an etc/X11 directory tree in /tmp and restores all the files from the tar archive into that directory. The tar command strips off the leading / from the filenames in the archive and restores the files in the current directory. If you want to restore the /etc/X11 directory from the archive on the floppy, use the following command:

```
tar zxvf /dev/fd0 /
```

The / at the end of the command denotes the directory where you want to restore the backup files.

As you can see, the tar command enables you to create, view, and restore an archive. You can store the archive in a file or in any device that you specify with a device name.

## Backing up and restoring a multivolume archive

Sometimes the capacity of a single storage medium is less than the total storage space needed to store the archive. In that case, you can use the M option for a multivolume archive — meaning that the archive can span multiple tapes or floppies.

> You cannot create a compressed, multivolume archive. That means you cannot use the z option.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_324_0.png)

To see how multivolume archives work, log in as root, place one disk in the floppy drive, and type the following tar command:

```
tar cvfM /dev/fd0 /usr/doc/ghostscript*
```

Note the M option in the option letters, which tells tar to create a multivolume archive. The tar command prompts you for a second floppy when the first one fills to capacity. Take out the first floppy and insert another floppy when you see the following prompt:

```
Prepare volume #2 for `/dev/fd0` and hit return:
```

When you hit Enter, the tar program continues with the second floppy. In this example, you need only two floppies to store the archive. For larger archives, the tar program continues to prompt for floppies in case more floppies are needed.

To restore from this multivolume archive, type cd /tmp to change the directory to /tmp and then type:

```
tar xvfM /dev/fd0
```

The tar program prompts you to feed the floppies as necessary.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_325_0.png)

Use the du -s command to determine the amount of storage you need to archive a directory. For example, here’s how you can get the total size of the /etc directory in kilobytes:

```
du -s /etc
8040      /etc
```

The resulting output shows that the /etc directory requires at least 8,040K of storage space to back up. If you plan to back up on multiple high-density floppies, you need about 8,040/1,200 = 7 floppies.

## Backing up on Tapes

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_325_1.png)

Although backing up on tapes is as simple as using the right device name in the tar command, you do need to know some nuances of the tape device to use it well. When you use tar to back up to the device named /dev/st0 (the first SCSI tape drive), the tape device automatically rewinds the tape after the tar program finishes copying the archive to the tape. The /dev/st0 device is called a rewinding tape device because it rewinds tapes by default.



Another good practice is to verify your backup automatically immediately after the tar archive is created. This is easily accomplished by tacking on the `-W` option, as shown in Listing 12.11.

### Listing 12.11 Using tar to verify backed-up files automatically

```console
$ tar -Wcvf ProjectVerify.tar Project4?.txt
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
Verify Project42.txt
Verify Project43.txt
Verify Project44.txt
Verify Project45.txt
Verify Project46.txt
$
```

You cannot use the `-W` option if you employ compression to create a tarball. However, you could create and verify the archive first and then compress it in a separate step. You can also use the `-W` option when you extract files from a tar archive. This is handy for instantly verifying files restored from archives.

Table 12.4 lists some of the options that you can use with the tar utility to restore data from a tar archive file or tarball. Be aware that several options used to create the backup, such as `-g` and `-W`, can also be used when restoring data.

### Table 12.4 The tar command's commonly used file restore options

| Short | Long | Description |
|:---|:---|:---|
| `-x` | `--extract` | Extracts files from a tarball or archive file and places them in the current working directory |
| | `--get` | |
| `-z` | `--gunzip` | Decompresses files in a tarball using gunzip |
| `-j` | `--bunzip2` | Decompresses files in a tarball using bunzip2 |
| `-J` | `--unxz` | Decompresses files in a tarball using unxz |

Extracting files from an archive or tarball is fairly simple using the tar utility. Listing 12.12 shows an example of extracting files from a previously created tarball.

### Listing 12.12 Using tar to extract files from a tarball

```
$ mkdir Extract
$
$ mv Project4x.tar.gz Extract/
$
$ cd Extract
$
$ tar -zxvf Project4x.tar.gz
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
$
$ ls
Project42.txt Project44.txt Project46.txt
Project43.txt Project45.txt Project4x.tar.gz
$
```

In Listing 12.12, a new subdirectory, Extract, is created. The tarball created back in Listing 12.6 is moved to the new subdirectory, and then the files are restored from the tarball. If you compare the tar command used in this listing to the one used in Listing 12.6, you'll notice that here the `-o` option was substituted for the `-c` option used in Listing 12.6. Also notice in Listing 12.12 that the tarball is not removed after a file extraction, so you can use it again and again, as needed.

![](img/c0a399aca0d18f8822d714ad0a173123_442_0.png)

> The tar command has many additional capabilities, such as using tar backup parameters and/or the ability to create backup and restore shell scripts. Take a look at the GNU tar website, www.gnu.org/software/tar/manual, to learn more about this popular command-line backup utility.

Since the tar utility is the tape archiver, you can also place your tarballs or archive files on tape, if desired. After mounting and properly positioning your tape, simply substitute your SCSI tape device filename, such as /dev/st0 or /dev/nst0, in place of the archive or tarball filename within your tar command.

## Duplicating with dd

The dd utility allows you to back up nearly everything on a disk, including the old Master Boot Record (MBR) partitions some older Linux distributions still employ. It's primarily used to create low-level copies of an entire hard drive or partition. It is often used in digital forensics for creating system images, for copying damaged disks, and for wiping partitions.

The command itself is fairly straightforward. The basic syntax structure for the dd utility is as follows:

```
dd  if=input-device of=output-device [OPERANDS]
```

The output-device is either an entire drive or a partition. The input-device is the same. Just make sure that you get the right device for out and the right one for in; otherwise you may unintentionally wipe data.

Besides the of and if, there are a few other arguments (called operands) that can assist in dd operations. Commonly used ones are described in Table 12.5.

### Table 12.5 The dd command’s commonly used operands

| Operand | Description |
| :--- | :--- |
| bs=BYTES | Sets the maximum block size (number of BYTES) to read and write at a time. The default is 512 bytes. |
| count=N | Sets the number (N) of input blocks to copy. |
| status=LEVEL | Sets the amount (LEVEL) of information to display to STDERR. |

The status=LEVEL operand needs a little more explanation. LEVEL can be set to one of the following:

- none only displays error messages.
- noxfer does not display final transfer statistics.
- progress displays periodic transfer statistics.

It is usually easier to understand the dd utility through examples. A snipped example of performing a bit-by-bit copy of one entire disk to another disk is shown in Listing 12.13.

### Listing 12.13 Using dd to copy an entire disk

```
# lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT

[..]
  sdb      8:16   0  4M 0 disk
   |sdb1   8:17   0  4M 0 part
  sdc      8:32   0  1G 0 disk
   |sdc1   8:33   0 1023M 0 part
[..]

# dd if=/dev/sdb of=/dev/sdc status=progress
8192+0 records in
8192+0 records out
4194304 bytes (4.2 MB) copied, 0.232975 s, 18.0 MB/s
#
```

In Listing 12.13, the `lsblk` command is used first. When copying disks via the `dd` utility, make sure the drives are not mounted anywhere in the virtual directory structure. The two drives involved in this operation, `/dev/sdb` and `/dev/sdc`, are not mounted. With the `dd` command, the `if` operand is used to indicate the disk we wish to copy, which is the `/dev/sdb` drive. The `of` operand indicates that the `/dev/sdc` disk will hold the copied data. Also, `status=progress` will display period transfer statistics. You can see in Listing 12.13 from the transfer statistics that there is not much data on `/dev/sdb`, so the `dd` operation finished quickly.

You can also create a system image backup using a `dd` command similar to the one shown in Listing 12.13, with a few needed modifications. The basic steps are as follows:

1. Shut down your Linux system.
2. Attach the necessary spare drives. You'll need one drive the same size or larger for each system drive.
3. Boot the system using a live CD, DVD, or USB so that you can either keep the system's drives unmounted or unmount them prior to the backup operation.
4. For each system drive, issue a `dd` command, specifying the drive to back up with the `if` operand and the spare drive with the `of` operand.
5. Shut down the system, and remove the spare drives containing the system image.
6. Reboot your Linux system.

If you have a disk you are getting rid of, you can also use the `dd` command to zero out the disk. An example is shown in Listing 12.14.

### Listing 12.14 Using dd to zero an entire disk

```
# dd if=/dev/zero of=/dev/sdc status=progress
1061274672 bytes (1.1 GB) copied, 33.196299 s, 32.0 MB/s
dd: writing to '/dev/sdc': No space left on device
2097153+0 records in
2097152+0 records out
1073741824 bytes (1.1 GB) copied, 34.6304 s, 31.0 MB/s
#
```

The `if=/dev/zero` uses the zero device file to write zeros to the disk. You need to perform this operation at least 10 times or more to thoroughly wipe the disk. You can also employ the `/dev/random` and/or the `/dev/urandom` device files to put random data onto the disk. This particular task can take a long time to run for large disks. It is still better to shred any disks that will no longer be used by your company.

## Replicating with rsync

Originally covered in Chapter 3, “Managing Files, Directories, and Text,” the `rsync` utility is known for speed. With this program, you can copy files locally or remotely, and it is wonderful for creating backups.

Before exploring the `rsync` program, it is a good idea to review a few of the commonly used options. Table 3.4 in Chapter 3 contains the more commonly used `rsync` options. Besides the options listed in Table 3.4, there are a few additional switches that help with secure data transfers via the `rsync` utility:

- The `-e`, or `-rs`, option changes the program to use for communication between a local and remote connection. The default is OpenSSH.
- The `-z`, or `--compress`, option compresses the file data during the transfer.

Back in Chapter 3 we briefly mentioned the archive option, `-a` (or `--archive`), which directs `rsync` to perform a backup copy. However, it needs a little more explanation. This option is the equivalent of using the `-rlptgoD` options and does the following:

- Directs `rsync` to copy files from the directory’s contents and for any subdirectory within the original directory tree, consecutively copying their contents as well (recursively).
- Preserves the following items:
  - Device files (only if run with super user privileges)
  - File group
  - File modification time
  - File ownership (only if run with super user privileges)
  - File permissions
  - Special files
  - Symbolic links

It’s fairly simple to conduct `rsync` backup locally. The most popular options, `-ahv`, allow you to back up files to a local location quickly, as shown in Listing 12.15.

### Listing 12.15 Using `rsync` to back up files locally

```bash
$ ls -sh *.tar
40K Project4x.tar   40K ProjectVerify.tar
$
$ mkdir TarStorage
$
$ rsync -ahv *.tar TarStorage/
sending incremental file list
Project4x.tar
ProjectVerify.tar
```


The type of backup to perform is specified using dump levels. Dump levels are specified numerically. Dump level zero indicates a full backup and dump levels 1-9 indicate that an incremental backup should be performed where all files modified since the last run with a level less than or equal to the specified dump level are archived.

To use dump to perform a backup, use the following syntax:

```
dump <dump level>usf <tape length> <tape device> <partition to back up>
```

The u flag indicates that dump should update `/etc/dumpdates` so that incremental backups are possible. Entries will be created in the `/etc/dumpdates` file of the form:

```
<partition> <dump level> <date and time>
```

For instance, the following entry indicates that the `/dev/sdb2` partition was backed up on December 27 and a full backup (dump level zero) was performed:

```
/dev/sdb2     0 Mon Dec 27 22:18:47 1999
```

The s flag in combination with the tape length value specifies the length of the tape being used in feet. If you don’t know the length of your tape, use an arbitrarily large number such as 650,000 because the default length is only 2,300 feet, which means that dump will prompt you to change your tape well before the tape is filled. Finally, the f flag in combination with the tape device indicates where the backup should be stored.

For instance, consider the following command:

```
# dump 9usf 650000 /dev/tape /opt
```

This command indicates that the partition mounted at /opt should be backed up to the tape device using a level 9 incremental backup.

The dump command generates output indicating the partition being backed up, the success of each stage of the backup, and the time taken to complete the backup, as illustrated in the following example:

```
# dump 0usf 650000 /dev/tape /opt
DUMP: Date of this level 0 dump: Tue Dec 28 22:14:04 1999
DUMP: Date of last level 0 dump: The epoch
DUMP: Dumping /dev/sda6 (/opt) to /dev/tape
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 14685 tape blocks on 0.34 tape(s).
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: 14852 tape blocks on 1 volumes(s)
DUMP: finished in 11 seconds, throughput 1350 KBytes/sec
DUMP: Closing /dev/tape
DUMP: DUMP IS DONE
```

## RESTORING FILES AND FILE SYSTEMS

The restore command allows you to restore files and directories from backups created with the dump command. The restore command can be used to recover an entire file system hierarchy from a level 0 dump and incremental dumps that follow it, or one or more files from one or more dump tapes.

![](img/6c13bcf02a08ad7923caab46f051d96a_183_0.png)

The restore command must be run by the root user, so that file ownerships, modes, and times can be restored to match the original files.

The following command will restore an entire file system hierarchy:

```sh
# restore rf /dev/tape
```

The r flag indicates that you want to restore an entire file system and the f flag along with /dev/tape specifies the source of the backup data.

The restore command can be used to restore files interactively using the i flag. When invoked with the i flag, the restore command provides an interactive shell where you can change directories within a backup set, list directory contents, and extract files.

Consider the following example where the file `/opt/src/amanda-2.4.1p1.tar.gz` is restored to the temporary `/restore` directory:

```text
# cd /restore
# mt rewind
# restore if /dev/tape
restore > ls
.:
lost+found/  src/
restore > cd src
restore > ls
./src:
README                  amanda-2.4.1p1.tar.gz  glibc22.patch
amanda-2.4.1p1/         glibc21.patch
restore > add amanda-2.4.1p1.tar.gz
restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you should start
with the last volume and work towards the first.
Specify next volume #: 1
set owner/mode for './'? [yn] n
restore > quit
# ls
lost+found  src
# cd src
# ls -l
total 697
-rw-r--r-- 1 root root 709624 Nov 21 1998 amanda-2.4.1p1.tar.gz
```

Within the interactive restore shell, two commands are critical:

- `add <filename>`: Adds a file to the set of files to be restored
- `extract`: Restores the specified set of files from the backup to the current location

## BACKING UP WITH AMANDA

Amanda is a freely available backup software program developed at the University of Maryland. The name AMANDA stands for Advanced Maryland Automated Network Disk Archiver. Its primary author is James da Silva of the University of Maryland.

Amanda is ideally suited to backing up medium and large networks. It allows you to perform network backup of multiple machines to a central backup server. Amanda uses GNU tar or the native dump program available with most Linux systems to perform backups. Used in conjunction with Samba, Amanda can also back up Windows 95 and NT machines.

The philosophy behind Amanda is to centralize backup of many machines onto a master tape server that has one or more tape drives and a large holding disk. Backup of many systems can be done over the network to the holding disk on the backup server. Several network backups can also be done in parallel. Once data has been backed up to the holding disk, it is written to a fast tape drive in a continuous streaming mode. This provides for efficient tape writing without tape interruption.

> **Note**
>
> Amanda can operate without a holding disk: Data from network clients can be written directly to tape but performance will be degraded and the total backup time can increase by several fold.

Amanda backup software is comprised of a suite of client and server software. Amanda provides its own networking protocols that run on top of standard UDP and TCP protocols. Currently Amanda uses UDP port 10080, and TCP ports 10082 and 10083 for communication between Amanda clients and servers. Amanda provides a very flexible data compression scheme that can be configured to compress data on the tape server to reduce load on the client machines, or to compress data on the clients and reduce network traffic between the clients and the tape server.

Amanda is a powerful piece of software; to fully understand and master it requires time. Consider subscribing to the Amanda mailing list by sending a message to `amanda-users-request@amanda.org`. This is a good resource for learning more about Amanda and getting help from other administrators running Amanda.

## BUILDING AMANDA FROM SOURCE

You can download the Amanda source code from `http://www.amanda.org`. The latest stable version at the time of this writing is 2.4.1p1. Amanda requires certain other software packages to be available on the system before compiling the software:

- GNU tar 1.12 or later version
- Perl 5.004 or later version
- GNU readline 2.2.1 or later version
- GNU awk 3.0.3 or later version
- Gnuplot 3.5 or later version

If you are going to back up Windows 95, 98, NT, or 2000 client systems using Amanda, you will also need to install Samba 1.9.18p10 or later version on the Amanda backup server.

### The Build Process

Use the following steps to install Amanda from the source code:

1. Download the Amanda archive and save it in a convenient location such as `/usr/local/src`. At the time of writing, the current version of the source code archive was `amanda-2.4.1p1.tar.gz`.

2. Change your current directory to `/usr/local/src`:

   ```
   # cd /usr/local/src
   ```

3. Extract the source code archive:

   ```
   # tar xzf amanda-2.4.1p1.tar.gz
   ```

   The source code will be extracted into the subdirectory `amanda-2.4.1p1`.

4. Change your current directory to the new subdirectory:

   ```
   # cd amanda-2.4.1p1
   ```

5. Configure the software with the following command:

   ```
   # ./configure --with-user=bin --with-group=backup \
   --with-tape-device=/dev/nst0 --with-amandahosts
   ```

   The `with-user` option specifies which user the software will run as, the `with-group` option specifies which group the software will run as, the `with-tape-device` option indicates the default tape device, and the `with-amandahosts` option indicates that an `.amandahosts` file will be used instead of an `.rhosts` in configuring Amanda. The user that is to run Amanda needs to have sufficient privileges to read and write to any tape drives you will be using; typical choices are bin, amanda, or backup for this purpose. Common group choices include backup, disk, or operator.

   This command will configure Amanda with a default backup configuration named Daily. If you want to use a different configuration name, add `--with-config=<your configuration name>` to the configure command. If you are compiling Amanda only to run on a client without needing to provide Amanda server capabilities, add the `--without-server` option to the configure command.

   By default, Amanda will be configured to install in the directories outlined in Table 10.1.

**Table 10.1 — Amanda Installation Directories**

| Directory | Description |
|---|---|
| `/usr/local/sbin` | Directory containing server-side binaries. |
| `/usr/local/libexec` | Directory containing client-side binaries. |
| `/usr/local/lib` | Directory containing Amanda (shared) libraries. |
| `/usr/local/man` | Directory containing the manual pages. |
| `/usr/local/etc/amanda` | Directory where the runtime files are found. Amanda supports multiple configurations per site; these are contained in subdirectories of this directory. |

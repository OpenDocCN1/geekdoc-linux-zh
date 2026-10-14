
| Table 13.7 tar Options |  |
|---|---|
| Option | Description |
| -c | Creates a new tar file |
| -x | Extracts from a tar file |
| -f filename | Specifies the file on which to perform an operation |
| -v | Specifies verbose output |
| -p | Retains file modes and ACLs |
| -t | Shows table of contents of specified tar file |

```
#tar -xvf /dev/rmt0 /home/restoredir
```

This command will extract the files from the tape and place them in the directory /home/restoredir. It should be noted that by default, tar does not restore files with the ownership and permissions on the original files unless you use the -p option:

```
#tar -xvp f /dev/rmt0 /home/restoredir
```

Table 13.7 shows a list of common tar options that can be used as part of your backup procedures.

![](img/415c89a1ede71e11e5040a0038b6916c_561_0.png)

## Platform-specific Backup Utilities

There was once a time when almost every UNIX platform used the commands dump and restore to back up files from disk to a specified tape medium. As UNIX evolved and matured, each flavor of UNIX migrated to its own variant of the dump and restore commands. Table 13.8 shows some of the different commands you can use to back up your UNIX platforms. Note that for all but Linux, each program works at the filesystem level. Before you run the commands below, make sure to read the man page thoroughly for any additional commands, or to determine if it is recommended to unmount a filesystem or bring the system to single-user mode.

Table 13.9 gives examples of the same commands that need to be used when restoring data from backup media. Something that is common to all of these commands is the -i option, which allows for interactive restores. If

you only need to capture a few files from the backup tape, the -i option allows you to navigate the directory structure on the tape and mark the files you wish to restore.

Using these commands is effective for a single system with an attached backup media device, or when backing up multiple systems to a single server. However, these commands fall short when you have a multi-vendor UNIX installation, or when you have to mange multiple backup servers to provide enough backup resources to effectively back up your environment. It should also be noted that almost all native UNIX backup utilities need to be configured in cron to run your backup schedule. Use cron, coupled with changes to the command line of each command, to provide you with your backup schedule for each day of the week.

- While there are a number of vendor backup packages that can help you manage large amounts of data and multi-vendor UNIX platforms, they can be very expensive to install on all of your UNIX systems. One alternative is the freeware package Amanda, which provides multi-platform backups and support for a wide array of backup media devices.

## Table 13.8 Platform-specific Backup Commands

| Platform | Backup Method | Backup Command Example |
|---|---|---|
| AIX | backup | backup -0 -u -f /dev/rmt0 / |
| HPUX | dump | dump 0df 6250 /dev/rmt/c0t0d0BEST / export/home |
|  | vxdump (Veritas filesystem) | vxdump 0bf 2097152 /dev/rmt/0m /mnt |
| Linux | BRU-2000 | BRU is actually GUI-driven |
| Solaris | ufsdump | ufsdump 5fuv /dev/rmt/1 /dev/rdsk/c0t3d0s6 |

## Table 13.9 Platform-specific Restore Commands

| Platform | Restore Method | Restore Command Example |
|---|---|---|
| AIX | restore | restore -i -f /dev/rmt0 |
| HPUX | restore | restore -i /dev/rmt/c0t0d0 |
|  | vxrestore | vxrestore -i /dev/rmt/0m |
| Linux | BRU-2000 | BRU is GUI-driven |
| Solaris | ufsrestore | ufsrestore -i /dev/rmt/1 |

## Multi-platform Backups Using Amanda

A very robust and powerful multi-vendor UNIX backup platform is the Advanced Maryland Automated Network Disk Archiver (known as Amanda), a project at the University of Maryland. Amanda will also support Windows platforms if you have SAMBA installed in your infrastructure. Information about this software package can be found at http://www.cs.umd.edu/projects/amanda/amanda.html. The latest distribution of the Amanda software can be downloaded from ftp://ftp.amanda.org/pub/amanda.

Once you've downloaded the distribution, you will need to compile and distribute the binaries for each UNIX platform you wish to back up, as well as install the software on the server(s) to which your backup media is attached. Amanda uses a combination of the tar command with gzip compression to perform backups. A central server is configured and remotely manages a list of servers that you define. You will need to create a trust relationship between the Amanda clients and the server for the UID that is responsible for running the backups. In almost every case, you will use the user operator to run the backups, and you will need to create an .rhosts file in /home/operator that contains the following:

```
#
#sample .rhosts file
#
backup.sniglets.com    operator
```

This will allow Amanda to use rsh to initiate the backup process on each remote system. Once the operator user is configured, you are ready to begin configuring and using Amanda. Some of the more frequently used Amanda programs are shown in Table 13.10.

Once you've installed the program, you will need to configure the amanda.conf file to reflect your infrastructure. While each line of

| Table 13.10 Commonly Used Amanda Commands |  |
|---|---|
| Command | Purpose |
| amdump | Performs a backup using Amanda |
| amlabel | Writes valid label to backup media so it can be catalogued by Amanda |
| amrestore | Extracts files from an Amanda tape |
| amcheck | Verifies the correct media is mounted and available |
| amadmin | Administers interface to Amanda |

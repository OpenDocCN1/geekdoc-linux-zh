
- 1. Checksum Verification - When archives are written, a checksum is calculated for each block of data. The checksum is stored in the header of the block. Checksum verification will read each block, recalculate the checksum, and compare the checksum to the value in the header. Each file will be listed as it is verified, along with any errors found. If no errors are found, you have an accurate backup.

- 2. Compare Verification - BRU compares the files to the archive on the hard drive. Any differences, such as modification times, size, or files in the archive that are nonresident on the hard drive are noted. An end of differences notice will be posted when the verification is complete.

## 7.1.12 Summary

For information on advanced features consult the BRU User's Guide or the BRU Web site at:

```
http://www.estinc.com/
```

## 7.2 Microlite BackupEDGE

BackupEDGE is a complete backup solution for the Linux platform. It is easy to use and still very robust. With BackupEDGE you can safely archive every file, directory, device node and special file on your file systems. Unlike the standard tar command, which ignores many important files, BackupEDGE also verifies every byte of data written to the tape to ensure the tape is an accurate reflection of your data. Below are the features provided by BackupEDGE software:

- Data compression - automatic data compression is supported.
- Menu interface - almost all functions can be accessed through an intuitive menu system.
- Remote tape drive support - you can back up computers across the network.
- High performance - advanced double buffering and variable block factors.
- Virtual file support - you can back up virtual (sparse) files.
- Multi-volume / Multi-device archives - automatic spanning across multiple volumes or devices.
- Wildcard support - when selecting files you can use a wildcard.
- Raw device backups - you can archive an entire raw device/partition to tape.
- Master / incremental backups
- Unattended operation - you can perform a master backup or back up only the changed files.

BackupEDGE is designed to operate on Linux kernels 2.x and there are available versions for several types of libraries.

In the following sections we describe how to install, configure and use the Microlite BackupEDGE backup software.

Note
We recommend that you do not connect tape devices to the IBM ServeRAID adapter. Use a separate SCSI controller for the tape devices.

### 7.2.1 Installing Microlite BackupEDGE

Before you install BackupEDGE you must identify the device entry for your backup device. Usually tape devices under Linux are assigned in device nodes /dev/st0, /dev/st1... A no-rewind device is created for each tape device, which is /dev/nst0, /dev/nst1... In our example, we used /dev/st0 as tape device and /dev/nst1 as the no-rewind device.

In our example, we used diskette as the installation media. To install the product, follow these steps:

- 1. Log in root.
2. Change the directory to root "/".
3. Insert the diskette with the product in the floppy drive and execute the command:
   tar xvf /dev/fd0
   Where /dev/fd0 is your floppy device.
4. Execute the following command to finish the installation:
   tmp/init.edge

You will see a window similar to Figure 188.

```
root@xxxx: ~ /
File Sessions Options Help
BackupEDGE Installation / Upgrade / Configuration

BackupEDGE 01.01.08 Installation Manager
This program will take you through the
steps required to install, upgrade, and/or
configure BackupEDGE on this system.

[Begin]                               [Exit]

(c) Copyright 1997-2000 by Microlite Corporation
```

**188.** Start of installation dialog

The installation program guides you through the installation process. The windows are intuitive. During the installation process, you can also configure your backup device(s) and your scheduling schema for unattended operation. If information is needed during this process, you are asked to enter the appropriate data.

Now you are ready to use the product.

The actions *Resource Manager* and *Defining Devices* can be started by entering on the command line:
`/usr/lib/bin/edge.resmgr` (Resource Manager) or
`/usr/bin/edge.config` (Defining Devices)

You can also perform these actions, if you click **Admin** on BackupEDGE main window.

### 7.2.2 Initializing the tape

Before you start making backups you should initialize the tape. To do this, you follow these steps:

- 1. Start the edgemenu program by executing command:

`edgemenu`

You will see a window similar to Figure 189.

```
[File] [Backup] [Restore] [Verify] [admin] [Schedule]

[File] [Backup] [Restore] [Verify] [admin] [Schedule]

[Define Resources]
[Resources]
[Reheat Backup Resources]
[Initialize Tape]
Changer Control
Activate BackupEDGE
DLT Registration
[Wake RecoverEDGE Media]
Do BackupEDGE Initialization

Primary Resource : n5500 drive DLT (/dev/sto0) (DLT Tape 35/70GB)
Overflow Resource: NONE
Changer Resource: NONE
Primary Compress: Hard. Tape Block: -1. Edge Block: 64. Partition: -1
Overflow: N/A
Last Master Backup: Tue Nov 2 14 20 15 1999
Local Machine  : n5500 first itso.com Administering n5500 first itso.com
```

Figure 18. BackupEdge main menu

2. In the Admin menu select Initialize Tapes. You will see a window to 190.

```
[File] [Backup] [Restore] [Verify] [admin] [Schedule]

[File] [Backup] [Restore] [Verify] [admin] [Schedule]

Initialize Tape in Primary Resource

[Initialize Tape]

Primary Resource : n5500 drive DLT (/dev/sto0) (DLT Tape 35/70GB)
Overflow Resource: NONE
Changer Resource: NONE
Primary Compress: Hard. Tape Block: -1. Edge Block: 64. Partition: -1
Overflow: N/A
Last Master Backup: Tue Nov 2 14 20 15 1999
Local Machine  : n5500 first itso.com Administering n5500 first itso.com
```

Figure 190. Initializing the tape

Chapter 7. Backup applications install and setup 193

3. Select Initialize Tape and press Enter. The tape will be initialized. You will get a message that the tape is successfully initialized. Press Enter to continue.

You can check the tape properties by selecting Tape Label in the Verify menu. You will see a window similar to Figure 191.

![](img/4e6a76e57a410be55d8a1cc0750b023_205.png)

### 7.2.3 Your first backup

In this section we will show how to make backups of desired files or directories. You can perform backups in the edgemenu utility. Follow these steps to make a sample backup:

- 1. Start the edgemenu program by executing the following command:
  /usr/bin/edgemenu
  You will see a window similar to Figure 192.

```
[File] [Backup] [Restore] [Verify] [admin] [Schedule]
[Master Backup]
  Incremental Backup
  All Files
  Backup Current Dir:
  Individual Files or Directories
```

Primary Resource: D5500 drive DLT (/dev/std) (DLT Tape 35/70GB)
Overflow Resource: NONE
Changer Resource: NONE
Primary: Compress Hard. Tape Block: -1. Edge Block: 64. Partition: -1
Overflow: N/A
Last Master Backup: Tue Nov 2 14 20 15 1999
Local Machine: n5500 first itso.com Administering: n5500 first itso.com
```

Figure 192. Starting the backup

2. In the Backup menu select Backup Files / Dirs, you will see a window similar to Figure 193.

```
[File] [Backup] [Restore] [Verify] [admin] [Schedule]
Master. Incremental, or Files Backup
Files / Directories Backup
Verify Volume: Record Locking
[S] Verify Type (File by File) (X) Don't Lock Files
[X] Index Directory Verifying ( ) Unforced Read
Files to include while processing archive read
Files / Directories to Include
/usr/src/
List File for Includes
```

```
Primary [ok] [Cancel]
Overflow: NONE
Changer Resource: NONE
Primary: Compress Hard. Tape Block: -1. Edge Block: 64. Partition: -1
Overflow: N/A
Last Master Backup: Tue Nov 2 14 20 15 1999
```

Figure 193. Selecting source for backup

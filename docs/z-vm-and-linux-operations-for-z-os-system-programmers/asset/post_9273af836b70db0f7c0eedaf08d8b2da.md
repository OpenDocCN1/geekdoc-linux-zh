
DFSMSdss dump can also be used to perform z/VM backup. In this case, a necessary physical dump must be performed in which you specify the tracks range to be copied.

## z/OS analogy: The following JCL is an example of a job to back up a z/VM disk (3390-03) from z/OS using DFSMSdss dump:
```
//STEP1  EXEC PGM=ADDRSSU,REGION=0M
//IDIOT   DD  DISP=(NEW,CATLG),DSN=backup.dsn........
//SYSPRINT DD  SYSOUT=* 

DUMP TRACKS(0,0,3338,14) -
INDY(LX6RES) OUTDD(IDIOT) ADMINISTRATOR CPVOLUME
```

## 8.4.2 z/VM online backups

Online backups can also be called hot backups. They do not require the system to be shut down before performing the backup.

### Using SPXTAPE to backup spool files

You may back up spool and system data files (that are printer, reader, and punch files) and saved segments, NLS files, and image libraries to tape by using the CP command SPXTAPE.

The SPXTAPE command allows you to selectively backup to tape and restore to disk spool and system data files. All files can be dumped, or a filter applied to only save the matching files.

### Copying z/VM CPOWNED minidisks

You may perform a hot backup of a running z/VM system by copying z/VM system disks. This is a non disruptive backup, because the system continues to run while the disks are copied.

Each CPOWNED disk has a corresponding fullpack MDISK definition in the MAINT user directory, as shown in Example 8-22.

> Note: CPOWNED disks added after z/VM installation should also be added as fullpack MDISKs in MAINT USER DIRECTORY for consistency.

### Example 8-22 CP owned disks, and corresponding MDISKs definitions

```
Ready; T=0.01/0.01 15:35:36
q cpown
Slot  Vol-ID  Rdev  Type  Status
1  LX6RES  1A20  Own  Online and attached
2  LX6SPL  1A21  Own   Online and attached
3  LX6PAG  1A22  Own   Online and attached
4  LX6W01  1A23  Own   Online and attached
5  LX6W02  1A24  Own   Online and attached

Ready; T=01/01.01 15:35:38
q v da
DASD 0122 3390 LX6SPL R/W      3339 CYL ON DASD 1A21 SUBCHANNEL = 000A
DASD 0123 3390 LX6RES R/W      3339 CYL ON DASD 1A20 SUBCHANNEL = 000B
DASD 0124 3390 LX6W01 R/W      3339 CYL ON DASD 1A23 SUBCHANNEL = 000C
DASD 0125 3390 LX6W02 R/W      3339 CYL ON DASD 1A24 SUBCHANNEL = 000D

Ready; T=01/01.01 13:35:12
```

These minidisks can be copied onto a new set of disks by using DDR, or Flashcopy if enabled. Example 8-23 shows the set of inputs required to copy the first disk.

### Example 8-23 Copying z/VM disks using DDR

```
ddr
z/VM DASD DUMP/RESTORE PROGRAM
ENTER:
IN 123 3390
ENTER:
OUT 1B34 3390
ENTER:
COPY ALL
HCPDDR711D VALID READ IS LX6RES
DO YOU WISH TO CONTINUE? RESPOND YES, NO OR REREAD:
YES
HCPDDR711D VALID READ IS DK1B34
DO YOU WISH TO CONTINUE? RESPOND YES, NO OR REREAD:
YES
COPYING  LX6RES
END OF COPY
ENTER:

END OF JOB
PRT FILE 0172 SENT FROM MAINT    PRT WAS 0172 RECS 0006 CPY 001 A NOHOLD
NOKEEP
Ready; T=09/1.13 13:41:07
```

All z/VM CPOWNED disks should be copied, with the exception of the paging disks that can simply be formatted and allocated as a paging device. This paging device must, however, have the same label that the existing paging device has, otherwise the copied z/VM system will not IPL correctly.

> Note: A good practice is to change the system DASDs labels after you have copied your z/VM system. Refer to 4.3.3, "Relabeling the system volumes" on page 165 for more details.

This copy operation results in a brand new z/VM system, ready to IPL. The IPL must be FORCEd, because no warm-start data was recorded. For more information about warm-start data, refer to 5.2.1, "z/VM IPL workflow" on page 230.

> Important: Although spool files such as the reader, printer or punch files can be lost during the copy process, this should not cause a problem restarting z/VM and the Linux virtual machines that were running in the environment.
> 
> This method cannot be applied to backups of running Linux machines. Back up of running Linux machines can lead to data inconsistency.

## 8.4.3 Linux backup tools

Linux distributions include tools for backing up and restoring data. Several are basic tools, such as tar or cpio; others are more complex, such as IBM Tivoli Storage Manager.

Although this section introduces several tools provided by the Linux distributions to perform backups, it is by no means a complete list.

> Important: All the tools described in this section do not perform consistency checks or data integrity control.

### Tar archiving utility

The tar utility is a standard UNIX tool to create an archive from a set of files or directories. This archive can then be compressed and saved to another set of disk or a tape. See Example 8-24.

Example 8-24 Archiving files using tar

```
lnxquill:"# tar cvf varlog_backup.tar /var/log
tar: Removing leading '/' from member names
/var/log/
/var/log/yaST2/
/var/log/yaST2/y2logRPM
/var/log/yaST2/y2log
/var/log/yaST2/y2logmkinitrd
/var/log/yaST2/y2log_bootloader
```

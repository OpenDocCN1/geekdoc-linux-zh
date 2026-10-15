DFSMSdss dump can also be used to perform z/VM backup. In this case, a necessary physical dump must be performed in which you specify the tracks range to be copied.

# z/OS analogy: The following JCL is an example of a job to back up a z/VM disk (3390-03) from z/OS using DFSMSdss dump:

```
//STEP1  EXEC PGM=ADDRSSU,REGION=0M
//IDIOT   DD  DISP=(NEW,CATLG),DSN=backup.dsn........
//SYSPRINT DD  SYSOUT=* 

DUMP TRACKS(0,0,3338,14) -
INDY(LX6RES) OUTDD(IDIOT) ADMINISTRATOR CPVOLUME
```

# 8.4.2 z/VM online backups

Online backups can also be called hot backups. They do not require the system to be shut down before performing the backup.

# Using SPXTAPE to backup spool files

You may back up spool and system data files (that are printer, reader, and punch files) and saved segments, NLS files, and image libraries to tape by using the CP command SPXTAPE.

The SPXTAPE command allows the you to selectively backup to tape and restore to disk spool and system data files. All files can be dumped, or a filter applied to only save the matching files.

# Copying z/VM CPOWNED minidisks

You may perform a hot backup of a running z/VM system by copying z/VM system disks. This is a non disruptive backup, because the system continues to run while the disks are copied.

Each CPOWNED disk has a corresponding fullpack MDISK definition in the MAINT user directory, as shown in Example 8-22.

> Note: CPOWNED disks added after z/VM installation should also be added as fullpack MDISKs in MAINT USER DIRECTORY for consistency.

# Example 8-22 CP owned disks, and corresponding MDISKs definitions

```
Ready; T=0.01/0.01 15:35:36
q cpown
Slot  Vol-ID  Rdev  Type  Status
1  LX6RES  1A20  Own  Online and attached
```
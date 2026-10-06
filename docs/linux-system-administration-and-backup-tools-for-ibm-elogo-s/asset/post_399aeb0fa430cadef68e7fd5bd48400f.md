
| Tape device | Arkeia | BackupEDGE | BRU |
|---|---|---|---|
| IBM 4/8 GB TR4 tape drive (SCSI-2 or EIDE) | x (only SCSI) | x | x |
| IBM 3447 DLT tape library (SCSI-2) | x | ? | | |
| IBM 3449 8 mm tape library (SCSI-2) | | ? | | |
| IBM 3575 Magstar MP tape library (SCSI) | x | ? | | |

For more information about the features of these tape devices, please consult Netinity Tape Solutions, SG24-5218, or the following websites:
http://www.ibm.com/storage
http://www.redbooks.ibm.com/

# Notes

Since Linux supports all SCSI devices, Linux should not depend on the technical characteristics of the tape drive used (for instance AIT, DAT, DLT, Exabyte, LTO, or QIC).

If you use tape libraries or auto changers, please enable the kernel option to probe all LUNs on each SCSI device. The tape drive and the changer may use the same SCSI-ID, but different LUNs.

We recommend you do not connect tape devices to the IBM ServeRAID adapter. Use a separate SCSI controller for the tape devices.

# 6.2 Backup strategy

The first issue to resolve is to determine what data to back up and when. Your first backup must be a full backup of your system. This can take a long time and require more than one backup medium depending on the amount of data to be backed up. These dependencies influence when you can run a full backup. After this full backup, you can run incremental backups, which means backing up only those files that have changed after the last or incremental backup. It is good practice to use different backup media for full and incremental backups. But take into account that restoring the data after a system crash requires the last full backup and all following incremental backups in their correct order. Since this can be very time consuming, you should plan a scheme for periodic backups very carefully. A suitable scheme may be one full backup per week during off hours and incremental backups on the other days. Whether you need more than one incremental backup per day depends on the amount of data that has changed and how critical your data may be.

For your full backup use the scheme Grandfather - Father - Son. This means, that you have three generations of backup data. During the new backup, when the grandfather becomes the new son, you have at least two generations of data to use, if the system crashes during this operation. If the creation of a new backup finishes successfully, the media for incremental backup can be reused again.

# 6.3 Backup tools

To back up your data, you can use one of the archiving tools that are already available on your system. Tar, cpio, dump are some of these tools. But take into account that you have a lot to do to use one of these tools comfortably.

You should consider one of the third-party products we mentioned earlier (BRU, Arkeia, or BackupEDGE/RecoverEDGE) for your backup tool. They come with a line interface, so you have full control over the tools' function, and you also have the use of a graphical interface. These products should include a scheduler to make it easier for you to set up the periodic scheduling most comfortable for you.

Information on the commercially available backup solutions can be found at the following websites:

- Arkeia: http://www.arkeia.com
- BRU/CRU: http://www.estinc.com
- BackupEDGE/RecoverEDGE: http://www.microlite.com

Detailed information on the installation and configuration of products on IBM xServer xSeries and Netivity servers can be found in Chapter 7, "Backup applications and setup" on page 181:

# 6.3.1 BRU and CRU

BRU (Backup and Recovery Utility) is the backup and restore solution from Enhanced Software Technologies (Web site: www.estinc.com). It is a backup and restore utility with significant enhancements over other common utilities such as tar, cpio, volcopy and dump. BRU is designed to work with most backup devices, including cartridge, 4mm DAT, 8mm (Exabyte) and 9-track tape drives.

BRU includes incremental backups, full backups, multivolume archives, distribution and updates, error detection and recovery, random access capabilities, file comparisons, and file overwrite protection.

As part of the package, BRU also contains a graphical user interface (GUI) named XBRU. From the command line, BRU is very similar to Tar. The dialog windows of XBRU are very intuitive and easy to use. To set up a schedule for scheduled backups, it is easiest to use the BRU for X11 Scheduler component of XBRU.

CRU (Crash Recovery Utility) is the recovery solution from Enhanced Software Technologies. It allows you to recover your system after a disaster crash.

To use CRU, you must create two floppy disks (a boot disk and a root disk) and/or a bootable CD-ROM, which are used to start the system recovery after a disaster crash. Follow the instructions in the CRU documentation to create the boot media. After every change in the system layout, mainly the layout of the hard disks, you must repeat the creation of the CRU boot and root disks.

CRU requires that you create a special backup tape using CRU. This backup feature of CRU can replace the corresponding BRU feature to create full backups.

# 6.3.2 BackupEDGE and RecoverEDGE

BackupEDGE is the backup and restore solution from MicroLite (Web site: www.microlite.com). It supports SCSI and also tape libraries.

RecoverEDGE is the recovery solution from MicroLite. It allows you to recover your system after a disaster crash. It allows you to create two floppy disks (a boot disk and a root disk) and/or a bootable CD-ROM, which are used to start the system recovery after a disaster crash.

# 6.3.3 Arkeia

Arkeia is a backup and restore solution that allows client/server architecture. It supports UNIX, Windows or Novell clients.

The following are features provided by Arkeia:

- Data compression
- GUI and CLI interface
- High performance
- Virtual file support
- Multi-volume archives
- Wildcard support
- Raw device backups
- Master / incremental backups
- Unattended operation

| Tape device | Arkeia | BackupEDGE | BRU |
|---|---|---|--|
| IBM 4/8 GB TR4 tape drive (SCSI-2 or EIDE) | x (only SCSI) | x | x |
| IBM 3447 DLT tape library (SCSI-2) | x | ? | |
| IBM 3449 8 mm tape library (SCSI-2) | | ? | |
| IBM 3575 Magstar MP tape library (SCSI) | x | ? | |

For more information about the features of these tape devices, please consult Netinity Tape Solutions, SG24-5218, or the following Web sites:
http://www.ibm.com/storage
http://www.redbooks.ibm.com/

# Notes

Since Linux supports all SCSI devices, Linux should not depend on the technical characteristics of the tape drive used (for instance AIT, DAT, DLT, Exabyte, LTO, or QIC).

If you use tape libraries or auto changers, please enable the kernel option to probe all LUNs on each SCSI device. The tape drive and the changer may use the same SCSI-ID, but different LUNs.

We recommend you do not connect tape devices to the IBM ServeRAID adapter. Use a separate SCSI controller for the tape devices.

# 6.2 Backup strategy

The first issue to resolve is to determine what data to back up and when. Your first backup must be a full backup of your system. This can take a long time and require more than one backup medium depending of the amount of data to be backed up. These dependencies influence when you can run a full backup. After this full backup, you can run incremental backups, which means backing up only those files that have changed after the last or incremental backup. It is good practice to use different backup media for full and incremental backups. But take into account that restoring the data after a system crash requires the last full backup and all following

Chapter 6. Backup and recovery 177
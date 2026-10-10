
## Target Server Agents (TSAs) and Workstation TSAs

- Target Server Agents (TSAs) are loaded on target servers and communicate with the backup program running on the host server. The purpose of the TSA is to get information from the target server’s volumes and send it to the SBCON utility running on the host server. A server can act as host and target by running both SBCON and TSA software.
- Workstation TSAs run on DOS or OS/2 workstations to back up data on local drives across the network.

In addition to the SBCON Storage Management Engine (SME) that ships with NetWare 6.5, a number of other companies offer specialized SME software packages with several features and benefits. The most common third-party backup systems are ARCServe and Backup Exec.

## Establishing a Backup System

Having a reliable and tested backup system is one of the best medicines a network administrator can have to ensure a good night’s sleep, so spending some extra time planning and testing the backup system is well worth it. Establishing a successful backup system involves six steps:

- Determine your network’s storage needs.
- Determine a backup strategy.
- Assign a backup user.
- Run the backup software on a scheduled basis.
- Test the backup.
- Develop a disaster recovery procedure.

In the following sections, you learn how Eric applied these steps to setting up the backup system for Universal AeroSpace.

## Determining Storage Needs

The first step in establishing a backup system for your network is to calculate how much data needs to be copied to the backup tape on a daily basis by determining which volumes and directories you plan to back up. If possible, you should try to obtain an SMS-compatible tape backup system with enough capacity to store your daily backup on one tape cartridge. In a single-file server environment, the file server acts as both the host and target device, requiring you to load the SBCON and TSA modules on the same server. An advantage of having a file server as both host and target devices is that a file server backing up its own data runs almost four times faster than a host file server backing up data across the network from another target server. As a result, when using SMS in a multiple-file server environment, you should plan on making the server that stores the most data the host system.

## Determining a Backup Strategy

Depending on your backup storage needs, one of the three backup strategies shown in Table 11-3 are normally used.

| Type of Backup | Data to Back Up | Status of Archive Attribute |
|---|---|---|
| Full | All data, regardless of when or if it has been previously backed up | Cleared |
| Incremental | Files created or modified since the last full or incremental backup | Cleared |
| Differential | All data modified since the last full backup | Not cleared |

With the **full backup** strategy, all data is copied to the backup tape each night. This backup strategy will work well for Universal AeroSpace because the current size of files to be included on the backup doesn’t exceed one tape cartridge. The advantage of the full backup strategy is that if a crash occurs, only the previous day's backup needs to be restored. The disadvantage is the need for a large tape capacity and the time required to perform backups.

The **incremental backup** strategy takes the least amount of time for each backup because only the data files that have changed that day are copied to the backup tape. When using the incremental backup strategy, a full backup is made at the beginning of the week, and an incremental backup is made each day. The disadvantage of this strategy is that all incremental backup tapes must be restored if data is lost. For example, if a crash occurs on Thursday, you need to restore the Monday full backup first, followed by the Tuesday and Wednesday incremental backups.

A compromise between the full backup and the incremental backup is the **differential backup** strategy, in which all files that have changed since the last full backup are copied to the backup tape. That means the size of the tape backup increases as the week progresses. The advantage of the differential strategy is that if a crash occurs later in the week, only the full backup and the last day's differential backup need to be restored.

Currently, Universal AeroSpace is using the full backup strategy to make a complete backup of all data and the eDirectory database each day. In the future, as UA's data storage requirements grow beyond the space of one tape cartridge, Eric recommends using the differential backup strategy to reduce the backup time and eliminate the need for someone to change tapes in the middle of the night.

## Assigning a Backup User

Although you can log in as Admin to perform a backup, most network administrators prefer to create a separate user account for backups. Creating a separate user account has the advantage of allowing you to assign other people to perform the backup and limits the number of times you need to log in to the network as Admin. The user account you create to perform the backup must have the following access rights and privileges:

- To back up the file system, the user account needs to have Read, File Scan, and Modify rights to the volumes and directories included in the backup. The Modify right is necessary for the backup program to reset the Archive attribute after backing up data files. When assigning these rights to the directory, you need to be aware of any IRFs (Inherited Rights Filters) that might block these rights from a subdirectory you want to back up.
- To back up the eDirectory database, the backup user account needs to have the Browse entry and Read attribute rights to the containers included in the backup.
- The person performing the backup needs to know the password used on the host server and the passwords assigned to any target servers or clients.

## Running the Backup Software

After you have decided on a backup strategy and created any necessary user accounts, the next step is to test the SMS installation by backing up your server data and then testing the backup by restoring selected files from the backup tape. The following steps outline the process of using SBCON to back up files:

![](img/840007e8f98ea6653e5877e945c27dc6_498_0.png)

1. Install Storage Management System (SMS) on your NetWare 6.5 server. To start, insert the NetWare 6.5 Products CD into the server's CD-ROM drive and then click the Novell button in the graphical interface to select the Install option.
2. Attach the backup device and load the appropriate drivers, as described in the backup device installation instructions.
3. Start SMS on the NetWare 6.5 server by typing SMSTART from the server console and pressing Enter. The SMSTART command loads the following modules:
   - The SMDR.NLM data requestor module automatically creates an SMS_SMDR. Group object in the server's container. This object contains each server and computer to be backed up by the host server.
   - The TSAP.NLM module enables you to back up data files and directories from this server.

You can also insert the SMSSTART command in the server's Autoexec.ncf startup file. (See Chapter 2 for a description of using the server startup files.)

4. In addition, you should also load the SMDI.NLM module in the Autoexec.ncf startup file by typing LOAD SMDI.NLM and pressing Enter. This command loads the SMS device module interface used to let the SBCON program communicate with the backup device.
5. Load the SBCON program on the host server by typing SBCON from the server console and pressing Enter to display the menu shown in Figure 11-25.

![](img/840007e8f98ea6653e5877e945c27dc6_499_0.png)

6. You can use the Job Administration menu item to display the Select Job screen, which you can use to perform backup and restore tasks, as shown in Figure 11-26.

![](img/840007e8f98ea6653e5877e945c27dc6_499_1.png)

7. Select Backup to display the Backup Options screen shown in Figure 11-27. You can use this screen to select the target server to be backed up, the directory or volume to back up, and the device or medium to use.

![](img/840007e8f98ea6653e5877e945c27dc6_499_2.png)

8. Select Advanced Options to select the backup type and time (see Figure 11-28).
9. You can use the Backup Type option to select a full, incremental, or differential backup. After making your selection, press Esc to submit the job and then return to the Select Job screen.
10. Press Esc again to return to the SBCON main menu. The backup job is then started at the time specified in the Advanced Backup Options screen.

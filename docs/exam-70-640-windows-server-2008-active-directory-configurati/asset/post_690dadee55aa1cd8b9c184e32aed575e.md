
The caching in step 1, in addition to the logging discussed in step 2, allows Active Directory to process multiple additional transactions before writing them to the database. When transactions are written to the database, it is more efficient to write multiple simultaneous transactions stored in the log file than to write each transaction individually.

Like any database, modifications and changes to the Active Directory database can affect database performance and data integrity. As modifications are made to the database, fragmentation can occur. **Fragmentation** refers to the condition of a disk when data from the database is divided into pieces scattered across the disk. As the database becomes more fragmented, searches for database information slow down and performance deteriorates. In addition, the potential exists for database corruption. A process called **defragmentation** is used to rearrange the information, making it easier to find during access requests and searches. *Defragmentation* is the process of taking fragmented database pieces and rearranging them contiguously to make the entire database more efficient. Depending on the method used, the size of the database can be reduced, making room for additional objects. Active Directory has two defragmentation methods: *online defragmentation* and *offline defragmentation*.

- **Online Defragmentation.** Online defragmentation is an automatic process that occurs during the *garbage collection* process. The garbage collection process runs by default every 12 hours on all domain controllers in the forest. When the garbage collection process begins, it removes all tombstones from the database. A **tombstone** is what is left of an object that has been deleted. Deleted objects are not completely removed from the Active Directory database; rather, they are marked for deletion. Tombstone objects have a lifetime of 180 days, by default. When the lifetime expires, the objects are permanently deleted during the garbage collection process. Additional free space is reclaimed during the garbage collection process through the deletion of tombstone objects and unnecessary log files. The advantage of an online defragmentation is that it occurs automatically and does not require the server to be offline to run. An online defragmentation does not reduce the actual size of the Active Directory database.

- **Offline Defragmentation.** Offline defragmentation is a manual process that fragments the Active Directory database in addition to reducing its size. Performing an offline defragmentation is not considered to be a regular maintenance task. You should only perform an offline defragmentation if you need to recover a significant amount of disk space. For example, if your domain controller no longer provides global catalog services in a forest, you might want to recover the disk space that once held the global catalog information. As its name suggests, offline defragmentation requires that the server be taken offline so that the Active Directory database is closed and not in use. An offline defragmentation cannot run while the AD DS service is running. In previous versions of Active Directory, this meant that you needed to restart a domain controller in a special startup mode called **Directory Services Restore Mode (DSRM)** to run an offline defrag. When a domain controller is restarted in DSRM, the Active Directory database is offline and the DC cannot service any client logon requests. In Windows Server 2008, Active Directory can now be started, stopped, and restarted, similar to any other service on a server, in a feature called **Restartable Active Directory Domain Services.** This allows administrators to perform certain operations, such as an offline defragmentation, without rebooting the domain controller in DSRM.

The following tasks should be performed before running an offline defragmentation:

- Back up the volume containing the Active Directory database, thereby backing up the current Active Directory database. Backup is discussed later in this lesson.
- Create a folder to temporarily store the compacted database.
- Verify that you have free space equivalent to the *size of the current database*, plus at least an additional 15 percent. This ensures that there is enough space for temporary storage during the defragmentation process and space for the newly compacted database.

## PERFORM AN OFFLINE DEFRAGMENTATION

**GET READY**. To perform these steps, you must have the Directory Services Restore Mode password available.

1. Restart your domain controller and press F8 after the BIOS information is displayed.
2. Select Directory Services Restore Mode (Windows Server 2008 domain controllers only) and press Enter.
3. Select the Windows Server 2008 operating system and press Enter.
4. Log on to Windows Server 2008 with the local Administrator account. This account is defined in the local computer database, not the Domain Administrator account.
5. From the Start menu, key cmd to open a Command Prompt window.
6. Key ntdsutil and press Enter.
7. From the Ntdsutil menu, key activate instance NTDS and press Enter. You will return to the Ntdsutil menu.
8. Key files and press Enter.
9. Key info and press Enter to view the current location of the Active Directory data files.
10. At the files prompt, key the following command, replacing drive and directory with the destination path for the compacted database:
    - `compact to drive:\directory`
11. Press Enter to initiate the creation of a new ntds.dit file in the specified directory.
12. Key quit and press Enter to exit the Ntdsutil utility. Key quit again to return to the Command Prompt window.
13. Copy the new ntds.dit file from the directory you specified in step 9 to the current Active Directory database path, which by default is C:\Windows\NTDS.

**PAUSE.** Restart your domain controller in normal mode.

You just performed an offline defragmentation of the Active Directory database. Next, we discuss the benefits and procedures for moving the database to a new location.

The decision to move the Active Directory database is usually driven by a need for additional disk space. The working database file system location must be updated in the registry—Ntdsutil does this automatically. If you are low on disk space on the drive where the original Active Directory database is stored, you can move the database to a different drive that has sufficient space. The difference in the outcome between the procedure for compacting the database, as discussed previously, and the procedure for moving the database is that when you move the database you must ensure that the registry keys provide the Active Directory database location are updated. If the registry keys that point to the file system location of Active Directory are not updated, Active Directory is not able to start. When the database is compacted, it is compacted to a new location. On completion, it is moved to the working database location. The registry keys pointing to the path in the file system for the working database do not change.

Moving the database and the associated log files requires two separate move procedures. These procedures are discussed next.

> **TAKE NOTE**
> When specifying a path that contains spaces at the command line, enclose the entire path in quotes. For example, if the destination path is D:\New Database, the path that should be keyed at the command line is “D:\New Database.”

## MOVE THE ACTIVE DIRECTORY DATABASE AND LOG FILES

**GET READY.** To perform these steps, you must have the Directory Services Restore Mode password available.

1. As a precaution, back up the volume containing the Active Directory database. (Backup is discussed later in this lesson.)
2. Click **Start**, click **Administrative Tools**, and then click **Services**. The Services MMC snap-in is displayed.
3. Right-click **Active Directory Domain Services** and click **Stop**. The *Stop Other Services* window is displayed, indicating that if you stop the Active Directory Domain Services service, you will also stop additional services on the Windows Server 2008 computer.
4. Click **Yes** to stop these additional services.
5. From the **Start** menu, key **cmd** to open a command prompt window.
6. Key **ntdsutil** and press (Enter).
7. From the Ntdsutil menu, key **activate instance NTDS** and press (Enter). You will return to the Ntdsutil menu.
8. Key **files** and press (Enter).
9. Key **info** and press (Enter) to see the current file information for the Active Directory database and logs.
10. At the files prompt, key the following command, replacing *drive* and *directory* with the destination path where you will move the database:
    - `move DB to drive\directory`
11. Press (Enter) to move the database to the new location.
12. To move the Transaction log files, key the following command at the files prompt:
    - `move logs to drive\directory`
13. Press (Enter) to complete the command. Key **quit** and press (Enter), then key **quit** and press (Enter) a second time to exit the Ntdsutil utility and command line.
14. From the **Services** MMC snap-in, right-click **Active Directory Domain Services** and click **Start**.
15. Wait a few seconds and then refresh the **Services** MMC snap-in to confirm that the additional services have restarted successfully.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_266_0.png)

You can also start a domain controller in Directory Services Restore Mode by pressing F8 as the server is booting or by using the `bcdedit` utility from the command line. To restart the server in DSRM using `bcdedit`, key `bcdedit /setsafeboot dsrepair` and then restart the server. To restart the server normally, key `bcdedit /deletevalue safeboot` and then restart the server.

**PAUSE.** **CLOSE** the Services MMC snap-in before continuing.

After the database has been moved, you will need to back up the new volume containing the Active Directory database to ensure that you can restore the database to the correct path if a failure occurs. Backup and restore procedures will be covered in upcoming sections.

## Backing Up Active Directory

> One of the most essential duties of an administrator is ensuring that data and operating system information is backed up in case of a failure. Procedures that include the frequency of backups in addition to the type of information that needs to be backed up should be planned and implemented in every organization.

Depending on the number of servers in your organization, your plan may vary. For example, if you have only one domain controller in your environment that services logons and stores data, then you must back up this computer frequently in case of a failure. In another scenario that includes one domain controller and several member servers that are storing data and

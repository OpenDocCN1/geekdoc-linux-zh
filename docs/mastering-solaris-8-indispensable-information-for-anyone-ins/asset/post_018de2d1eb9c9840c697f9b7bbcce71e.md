
2. Select the user accounts you wish to see in the Set Initial View dialog box, then double-click any user account icon for which you want to grant, modify, or delete rights. The User Properties dialog box (shown in Figure 11.29) appears.

### FIGURE 11.29
*The Rights tab of the User Properties dialog box*

![](img/256e02a6afce528d264a8d911fa0ff20_497_0.png)

3. Click the Rights tab to display a list of rights for that account. On the Rights tab, you can assign to a particular user account rights that may be used for roles the user account may assume.
4. Select the check boxes next to the rights you wish to enable. Or, click the Enable All button to grant all rights to that user account.
5. Deselect the check boxes for the rights you wish to disable. Or, click the Clear All button to deny all rights to that user account.
6. Click the OK button to establish your selections.

Table 11.4 lists the rights that you can assign on the Rights tab of the User Properties dialog box.

### TABLE 11.4: ASSIGNABLE RIGHTS FOR ROLES

| Right Class | Specific Rights |
|---|---|
| Audit Management | Configure auditing, read audit trail |
| Device Allocation | Allocate device, configure device attributes, delegate device administration, revoke or reclaim device |
| Cron and At Jobs | Cron and at administration, delegate cron and at administration, create at or cron jobs |
| Login Control | Enable logins, remote login |
| Execution Profile Management | Assign profiles to users or roles; create, modify, delete profiles |
| Role Management | Assign roles to users; add, modify, delete roles |
| Machine Administration | Set date and time, shut down the system, manage file systems, mount/share file system |
| Computer/Networks | Write computer and network information |
| Log Viewer | Back up and delete log files, change log settings |
| Serial Ports | Delete serial ports, modify serial port information |
| User, Groups, & Mailing Lists | Change user passwords, add, modify, and delete |

## Summary

In this chapter, you learned about user and group accounts. Solaris uses a system of users and groups to allow access to system and network resources. The user and group databases store information about user accounts and group accounts.

User accounts have passwords, can expire, and are linked to a primary group and up to 16 secondary groups. Group accounts allow access and rights to files, directories, and other objects for a number of user accounts. User accounts are identified by a user identification (UID) number; group accounts are identified by a group identification (GID) number.

You learned how to create and manage local group and user accounts with the graphical Admin tool. After you create a new user account, you still need to specify a home directory and create a user environment for that account. This chapter also covered AdminSuite 3. As part of the Solaris Management Console, you can use AdminSuite 3 to modify user accounts and group accounts in a network environment.

## CHAPTER 12
## Working with File Utilities

FEATURING:

- Working with archives 480
- File compression 486
- File encryption 488
- Using packages for program installation 490
- Solaris backup and restore utilities 495
- Backup strategies 498

![](img/256e02a6afce528d264a8d911fa0ff20_499_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_499_1.png)

In this chapter, you’ll learn about a number of file handling utilities that are important in your daily work. Archives offer you method for combining files into a single file that can be more easily managed and handled. Archives are often used as a mechanism to transfer data between systems because they simplify the process. You’ll also learn how to work with tar files. Hand in hand with archives are compression utilities. Some archival utilities, such as GNU tar, offer compression and some do not. However, you will certainly want to make use of utilities like the compress command and GNU gzip to compress files and archives. Compression speeds up data transfer operations.

Much of this chapter describes how to back up and restore your directories and files and why it is so important for users and administrators alike. Solaris offers several commands, such as ufsrestore and ufsbackup, that allow you to back up and restore to tape drives and other devices. Unix is rich in command-line utilities for disk, directory, and file copy commands. Some of these commands are described in this chapter in the context of backing up and restoring. You will also find a discussion of backup strategies in this chapter, as well as a listing of different freeware and third-party backup programs that you might want to use with your systems.

## Archives

Archives provide a method for conveniently packaging files. They can also be used to back up a small amount of files. One of the oldest utilities in Unix is the tar command, which writes the tar output to a single disk file. Many people use tar files as a means of distributing file trees with other users. You may encounter tar files being used on the Internet as a transfer format. The tar command was originally used to create a tape archive, hence the name of the command. However, tar is often used to create a single file from a group of files and directories. Unlike utilities such as zip, tar does not offer file compression. However, tar files are often further compressed by applying commands like compress to archives after they are created and before they are used in file transfers.

To create a file using the tar command, do the following:

1. Use the cd (change directory) command to switch to the directory that contains the subdirectories and files you want to archive:
   ```
   # cd /usr/<directoryname>
   ```
2. Give the du (disk usage) command to determine the size of your archive.
   The du -a command returns the size of each file in blocks along with the total size of the directory. The -k flag will provide the output of the du command in KB, which is easier to understand. To suppress the listing of the directory size without listing individual components, use the du -s option.
3. Create your tar archive by giving the following command:
   ```
   # tar cvf <pathname>/<archive name>.tar *
   ```

This command creates a package that includes all of the subdirectories with the filename `<archive name>.tar` in the location of the `<pathname>`. An icon of an archive is shown in the following graphic.

![](img/256e02a6afce528d264a8d911fa0ff20_501_0.png)

The tar command is one of the most useful commands you will find because it allows you to “package” files together for further manipulation. Therefore, you might want to know about some of the more common options that tar supports; some of these options are shown in the following list (note that you can use r, t, u, and x only one time for each run of tar, and they can each be augmented by f and v, as in rf and rv, tf and tv, uf and uv, and xf and xv):

- **c option** Creates a new archive.
- **f `<device name>` option** The f option uses the `<device name>` as the name of the file created. When used with a hyphen, the command writes to or reads from standard output. The tar command can be used on either side of a pipe. When f isn’t specified, the command uses the device found in the TAPE environmental variable. When f is specified, the default values in the /etc/default/tar command is used.
- **r option** Appends files to the end of an existing archive.
- **t option** Displays a table of contents. It displays the list of files contained in the archive. The v option adds the file information to the filenames.
- **u option** Updates the archive by adding named files to it if they aren’t already contained in the archive or if they were modified since the archive was created. When you update, you also append.
- **v option** With the verbose option, tar echoes its operations.
- **x `<filenames>` option** Extracts or restores the files you specified from an archive to the current directory. When a filename matches a directory name,

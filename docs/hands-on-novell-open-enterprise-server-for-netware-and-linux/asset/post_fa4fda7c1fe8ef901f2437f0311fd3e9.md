
7. Follow these steps to record permissions for the products directory:
   - a. Click the **products** directory and click **Properties** to open the Properties dialog box.
   - b. Click the **Permissions** tab and record the permissions: _______________________________
   - c. Close the products directory window.

8. Use the procedure in Step 7 to record permissions for the facilities directory:
________________________________________________________________

9. Close Konqueror, and leave your system running for the next activity.

## Sharing and Accessing Network Files

As with any server operating system, one of the major functions of a Linux server is sharing data with client computers. In Linux, you can share directories with other Linux and UNIX systems by using the standard **Network File System (NFS)**. You can also share data with a Windows client by using the Samba service described in Chapter 14. In this section, you learn how to use NFS to share files on your Linux server.

Novell OES has NFS configured and ready to go. All you have to do is use YaST to start the service and add the directories you want shared on the network. To use YaST to enable NFS, use the following steps:

1. Start YaST and, if necessary, enter your root user password.
2. Click **Network Services** in the left pane to display the menu options. You can select NFS Client or NFS Server options. The NFS Server option is used to share directories, and the NFS Client option is used to mount remote directories.
3. To share a directory, click the **NFS Server** option in the right pane to open the Configuration of the NFS server dialog box.
4. Click the **Start NFS server** option button, and then click **Next** to display the *Directories to export to the others* dialog box (see Figure 13-30).

![](img/840007e8f98ea6653e5877e945c27dc6_566_0.png)

5. Click the **Add directory** Button and then use the **Browse** button to navigate to the EngData directory and then to the directory you want to share.
6. Click the directory to be shared, and then click **OK** to open the Hosts wildcard option dialog box, where you can change the wildcard symbol used when searching for files. In most cases, leave the default of the “$” character, and click **OK** to add the directory to the Directories to export to the others dialog box.
7. Click **Finish** to share the directory and return to the YaST Network Services menu.

## Activity 13-10: Using NFS to Share a Directory

**Time Required:** 10 minutes

**Objective:** Use NFS to share and mount remote directories.

**Requirements:** Completion of Activities 13-1 and 13-9 and a partner to test your NFS shared directory

**Description:** To allow users in the Engineering and Manufacturing departments to access the Linux server directories from their Linux systems, Eric wants you to share them by using NFS. In this activity, you share your EngWeb directory structure and then try to mount another student’s shared directory.

1. If necessary, log in to your SUSE Linux server with your user name and password.
2. Start YaST and, if necessary, enter your root user password.
3. Click the **Network Services** icon in the left pane, and then scroll down and click the **NFS Server** option in the right pane.
4. If necessary, click the **Start NFS server** option button, and then click **Next** to open the Directories to export to the others dialog box.
5. Click the **Add directory** button, and then click the **browse** button, click to select your **EngWeb** directory, and click **OK**.
6. Click **Finish** to save your changes and return to the Network Services window.
7. Follow these steps to mount your partner’s NFS directory after he or she has finished Step 6:
   - a. If necessary, start YaST and open the Network Services menu.
   - b. Click the **NFS Client** option in the right pane to open the Configuration of the NFS client dialog box (see Figure 13-31).

![](img/840007e8f98ea6653e5877e945c27dc6_567_0.png)

Figure 13-31 The Configuration of the NFS client dialog box

   - c. Click the **Add** button to open the dialog box shown in Figure 13-32.
   - d. Enter the IP address of your partner’s server in the Host name of the NFS server text box, select the remote file system and mount point, and click **OK** to mount the remote file system.
8. Close all applications, log out, and leave your system running for the end-of-chapter projects.

![](img/840007e8f98ea6653e5877e945c27dc6_568_0.png)

## CHAPTER SUMMARY

- Linux is a multiuser operating system that requires users to have a valid user name and password to access the system. Groups are used to grant rights to users and can be defined as system or local. Local groups are used to give users rights to data and applications; system groups are used to grant users rights to the operating system.

- The root user account has full control of the system and is a member of the root system group. Other users can be superusers by making them a member of the root group.

- The shell gives users a command-line environment for starting programs. Common shells include the Bash, Korn, and C shells. Users are given a default shell when their user account is created.

- User and group accounts can be created and managed in the YaST utility or with the useradd and groupadd commands.

- The man and info commands are used to retrieve help information on Linux commands. You can also get online help from a number of Web sites.

- Run levels are used to set a user's default environment when he or she logs in. Run level 5 provides a multiuser, networked graphical environment, and run level 3 is used for text-based operations.

- Red Hat Package Manager (RPM) is used to install and manage Linux applications from a compressed file. With RPM, you can determine software dependencies, install and test software, and perform automatic software updates.

- Linux supports a number of file systems, including ext2, ext3, and ReiserFS. ReiserFS offers the best performance for handling large numbers of small files and is the default file system in SUSE Linux.

- Disk partitions are the physical areas of the hard drive that are formatted to store data. Disk partitions are given names based on their disk drive and partition number.

- With logical volume management, disk partitions can be grouped into volume groups used to create logical volumes. Logical volumes are then mounted and used by the operating system.

- Volumes and other storage devices need to be mounted in the file system before they can be used. Logical volumes are mounted in the root partition of the file system, which is specified by a forward slash (/).

- The Linux file system has a simple security system that assigns rights to the file owner, associated group, and others. Rights include read, write, and execute. The read right is assigned a value of 4, the write right has a value of 2, and the execute right has a value of 1. These values are added to produce an octal digit representing the rights assignment.

- Linux directories can be shared with other Linux or UNIX systems by using NFS and with Windows systems by using Samba. NFS is a native Linux service that exports directories to the network. These exported directories can then be mounted in a remote computer's file system and accessed based on user rights.

## Key Terms

- **Enterprise Volume Management System (EVMS)** — An enhanced version of the Logical Volume Manager that supports Novell NSS volumes. *See also Logical Volume Manager.*
- **info pages** — Command-line documentation pages viewed with the *info* command. Info pages are newer than man pages and often contain more information.
- **inode** — An index entry containing information about a Linux file.
- **journaling file systems** — A file system that keeps a log of data transactions applied to a disk partition.
- **local groups** — Group accounts created by a Linux administrator and used to assign rights and permissions to users.
- **Logical Volume Manager (LVM)** — A volume management system used to group physical hard drive partitions into volume groups for the purpose of creating logical volumes.
- **man pages** — Command-line documentation pages viewed with the *man* command.
- **Network File System (NFS)** — A Linux file system server that allows exporting files and directories to the network for remote access.
- **RedHat Package Manager (RPM)** — A software installation file format used by the *rpm* command to install and manage software.
- **shell** — A Linux command-line environment used to enter commands and start programs.
- **system groups** — Group accounts that the Linux operating system creates to grant rights for accessing certain system resources.
- **Virtual Filesystem Switch (VFS)** — An operating system interfacing system that sends user requests from a process to the actual disk file system.
- **X-Window** — The interface used to provide graphical support that other software packages, such as the KDE and Gnome desktops, draw on.

## Review Questions

1. Which of the following system groups can be used to create a backup system administrator?
   a. admin
   b. root
   c. domain admin
   d. manager
2. The root user is assigned a user ID of ____________.
   a. 0
   b. 1
   c. 100
   d. 10
3. Which of the following is the default shell in SUSE Linux?
   a. Bourne
   b. Bourne Again (Bash)
   c. Korn
   d. C
4. Which of the following files does SUSE Linux use to store encrypted passwords?
   a. passwd
   b. system
   c. shadow
   d. password

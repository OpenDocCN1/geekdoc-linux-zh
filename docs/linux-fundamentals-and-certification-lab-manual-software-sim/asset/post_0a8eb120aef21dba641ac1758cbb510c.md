
### FIGURE 4–12
Group specifications Base info tab.

![](img/37f079cee226b270f2e09b37a2e4a05d_103_0.png)

The **Directories** tab (Figure 4–13) allows entry of the base directory that the group will be using. The default permission for the directory is 700, indicating that the owner has full access. Values required for group directories will be discussed later in this chapter.

### FIGURE 4–13
Group specification Directories tab.

![](img/37f079cee226b270f2e09b37a2e4a05d_103_1.png)

3. Click **Accept** to create the group.

### Assigning Users to Groups

After a group is created, users must be added to the group. This can be accomplished through use of the command line or the GUI. It is not uncommon for a user to belong to multiple groups.

From the command line type `usermod -G mygroup` where `mygroup` is the group to add. A user can be added to multiple groups by entering the group names followed by commas and no spaces.

### Using the Mandrake Linux GNOME GUI

1. Select Main Menu, Configuration, Userdrake, as shown in Figure 4–14. The Userdrake tool allows adding, modifying, and deleting users and groups.

![](img/37f079cee226b270f2e09b37a2e4a05d_104_0.png)

2. From the Userdrake dialog box (Figure 4–15), select the Settings menu, then View groups (Figure 4–16). A list of groups is displayed.

![](img/37f079cee226b270f2e09b37a2e4a05d_104_1.png)

3. Open the group to which users are to be added. You may have to scroll down the list to find the correct group.

4. After the group is selected, a dialog box with the same name as the group is displayed (Figure 4–16). The Identity tab is used to change the name of the group. Changing a group name can cause problems if other applications are using the group.

### FIGURE 4–16
Group dialog box, Identity tab.

![](img/37f079cee226b270f2e09b37a2e4a05d_105_0.png)

5. Select the **Users** tab.
6. Select usernames from the **Not in group** column; then click **Add** to place users in the **In group** column (Figure 4–17).

> **NOTE**
> Multiple usernames can be selected by holding down the Ctrl key while clicking each entry. To select a range of entries, click the first username and then click the last entry while holding down the Shift key.

### FIGURE 4–17
Group dialog box, Users tab.

![](img/37f079cee226b270f2e09b37a2e4a05d_105_1.png)

7. After usernames are added, select **OK**. In the Userdrake dialog box, click the **Save** button on the toolbar to save changes. If **Save** is not clicked, a dialog box will display and ask to confirm to quit Userdrake without saving (see Figure 4–18).

![](img/37f079cee226b270f2e4a05d_106_0.png)

After a user and group are created *the /etc/passwd* file contains the information. Within *the /etc/passwd* file is the login ID, UID, GID, login directory, and the default shell. View the */etc/passwd* file by typing `cat /etc/passwd`.

A second file contains the encrypted passwords for each user. *The /etc/shadow* file contains the username, the encrypted password, and information about password policy. View the */etc/shadow* file by typing `cat /etc/shadow`.

## MANAGING AND NAVIGATING THE LINUX FILE SYSTEM

The Linux file system is designed to organize data. A file system can easily contain thousands of files that must be organized in a fashion that makes them easy to locate. If a file cannot be found in the file system, it is the same as not having the file to begin with. Data on a Linux file system can be classified as sharable or unsharable, and static or variable.

Sharable files can be accessed by other hosts on the network. For example, a user in Accounts Payable can access the data for that department on the group's file server. The data is shared and available for the members of the group.

Unsharable files cannot be accessed by any other hosts on the network. Unsharable files can include system files, local configuration files, and other files that are used only on the local machine.

Static files are files that do not change, such as command documentation and program files. Static files are termed read-only files.

Variable files are files that change over time. These can include user configuration files, common data files for a work group, and other data that changes without system administrator intervention.

Understanding the nature of files on Linux helps you understand how files are associated with file permissions. A file can be read-only, read-write, and other combinations of permissions. The way a file is used by the system determines what permissions need to be applied to the file.

To help users find files within the file system, a standard exists that identifies where certain types of files go. This standard is the File system Hierarchy Standard (FHS, see http://www.pathname.com/fhs/) maintained by the File system Hierarchy Standard Group. The standard contains a set of requirements and guidelines for file and directory placement under Unix-like operating systems. Use of the FHS provides interoperability of applications, system administration tools, development tools, and scripts.

### Common Directories

The FHS defines many common directories used in Unix-like operating systems. The following lists some of these common directories; however, the FHS document includes other directories not listed here. Refer to the latest FHS document for a complete set of directories.

- **Root /** The root directory is the top of the file system hierarchy. The contents of the root file system must contain all the files needed to boot, restore, recover, and repair the system.
- **/bin** The /bin directory contains commands used by the system administrator and other users. These are required commands when no other file systems are mounted.
- **/boot** The /boot directory contains all files, except configuration files, needed to boot the operating system. The /boot stores data that is used before the kernel begins executing user-mode programs.
- **/dev** The /dev directory contains file system entries that represent devices that are part of the system.
- **/etc** The /etc directory contains local configuration files. No binaries are contained within /etc.
- **/home** The /home directory contains user directories. The /home directory is optional. Typically, the /home directory contains a subdirectory for each user added to the system.
- **/lib** The /lib directory contains shared library images needed to boot the system and run the commands in the root file system.
- **/opt** The /opt directory contains add-on application software packages.
- **/proc** The /proc file system is used to handle storage and retrieval of process information.
- **/root** The /root directory is the home directory of the root user.
- **/sbin** The /sbin directory contains utilities used for system administration.
- **/tmp** The /tmp directory contains temporary files. These files are automatically removed after a period of time.
- **/usr** The /usr directory contains files that can be shared across all hosts. This directory is mounted read-only and contains the following subdirectories or symbolic links to directories:
  - **/usr/bin** contains most user commands
  - **/usr/include** contains header files included by C programs
  - **/usr/lib** contains libraries
  - **/usr/local** local hierarchy for installation of nonstandard applications
  - **/usr/sbin** contains nonvital system binaries
  - **/usr/share** contains architecture-independent data
- **/var** The /var directory contains variable data files. This includes spool directories, log files, and temporary files. Some directories within /var are sharable and some are unsharable. The following directories are required in /var:
  - **/var/cache** contains application cache data
  - **/var/lib** contains variable state information
  - **/var/local** contains data for /usr/local

# Working with the Linux File System

After a file system has been created and formatted, it must be mounted in the root partition before it can be accessed. As described previously, file systems can be mounted automatically in the *fstab* file or manually with the mount command. When mounting a file system, first you need to create a directory off the root partition where the file system will be located. You can specify this location and the partition name with the mount command or in the *fstab* file. For example, to mount the sdb1 partition in a directory named *CorpData* located at the root of the file system, you could use the following commands:

+   - **su**—Switch to the root user.
+   - **mkdir /CorpData**—Create a directory for the file system off the root.
+   - **mount sdb1 /CorpData**—Mount the file system in the *CorpData* directory.

After the file system is mounted, you need to know some common Linux commands, listed in Table 13-10, to work with the Linux file system. In the following activity, you use these commands to mount your file system and then create a simple directory structure.

**Table 13-10 Common Linux file system commands**

| Linux Command | Description |
|---|---|
| ls | View directory contents |
| cp | Copy files |
| cd | Change directory |
| mkdir | Create a new directory |
| mv | Move or rename a file |
| rm | Delete the specified file |
| grep | Search for a specific string in a text file |
| tail | Display the last 10 lines of a text file |

![](bbox=[0.03, 0.5, 0.11, 0.57])

# Activity 13-7: Creating a Linux Directory Structure

**Time Required:** 10 minutes

**Objective:** Use basic Linux commands to view and work with the Linux file system.

**Requirements:** Access to the root user password for your Linux server

**Description:** Eric wants you to create a directory in the root of the Linux server's file system to provide a mount point for the Engineering Department's partition. In this activity, you learn how to use command-line utilities to create a directory off the root of your file system that will be used to mount the Engineering partition in Activity 13-8.

+   1. If necessary, log in to your SUSE Linux server with your user name and password.
+   2. Open a terminal window.
+   3. Type **su** and press **Enter** to switch to the root user. Type the root user's password and press **Enter** again.
+   4. Type **cd /** and press **Enter** to change to the / (root) directory.
+   5. Type **mkdir EngData** and press **Enter** to create the EngData directory.
+   6. View your directories by typing **ls** and pressing **Enter**.
+   7. Type **exit** and press **Enter** twice. You can stay logged in and leave your system running for the next activity.
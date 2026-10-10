
## Working with Network Files

Files are used to store data in the network file system in much the same way they’re used to store data and software on your local disk drives. Planning the location of files on network volumes is an essential part of organizing the file system. Although files can exist on the root of a volume, placing them in directories and subdirectories results in a more organized file system and increases file system security, as described in Chapter 6.

NetWare stores information about each file in the **directory entry table (DET)** located at the beginning of each volume. In addition to the file’s name and storage location, NetWare includes such information as owner, size, creation dates, access dates, trustee assignments, and attributes. By default, the file owner is the user who creates the file. By keeping track of file owner and size information, NetWare enables network administrators to limit disk space usage on a user-by-user basis. Network administrators also need creation and access dates to perform such functions as listing files that haven’t been accessed for a specified period.

## Salvaging Deleted Files

As discussed previously, one strength of NetWare’s file system is that files can be recovered reliably even after they have been deleted for a long time. When a file is deleted, NetWare does not overwrite its space until space from all previously deleted files has been reused. Deleted files are kept track of within the directory they were deleted from and can be salvaged from their parent directory. As a result, a user can often recover deleted files from the parent directory many months after the file has been deleted. Even if the entire directory structure that contained the file is deleted, the deleted files are still kept track of and can be recovered from the Deleted.sav directory by the network administrator.

![](img/840007e8f98ea6653e5877e945c27dc6_133_0.png)

Standard users do not have rights to salvage files from the Deleted.sav directory. Only the network administrator has this right by default.

For security reasons or for OS efficiency, however, sometimes you want to give deleted file space back to the OS immediately for reuse—a process called **purging files**. When files are purged, NetWare reclaims their space and they can no longer be recovered. As a result, purging deleted files can be important for security purposes because it prevents the deleted files from being salvaged. If purged files exist on an NSS volume and the Salvage attribute, described earlier in this chapter, is not enabled, purged files are overwritten with random patterns of characters to help make sure the deleted data can’t be accessed or viewed. Another advantage of purging files is to make space immediately available to the NetWare server for reuse. Purging not only increases NetWare’s efficiency, but also prevents other possibly valuable files from being reused as quickly. For example, say a user recently installed a software package in the Apps directory and then decided to delete the software directory and place it on her local computer. Purging files in the Apps directory makes any disk space used by the application files immediately available for other purposes. In the following activity, you practice using Remote Manager to work with network files.

![](img/840007e8f98ea6653e5877e945c27dc6_133_1.png)

## Activity 3-9: Deleting and Salvaging Network Files in Remote Manager

**Time Required:** 10 minutes

**Objective:** Manage network files with Remote Manager.

**Requirements:** A Windows XP system and successful completion of Activity 3-8

**Description:** In addition to managing volumes and directories, you can use Remote Manager to work with network files. In this activity, you practice using Remote Manager to upload a file, salvage deleted files, and purge deleted files.

- 1. If necessary, start Remote Manager using the IP address of your assigned NetWare 6.5 server.
- 2. Log in with your administrative user name and password.
- 3. Click the **Volumes** link under the Manage Server heading, and then click your assigned volume to display the directories.
- 4. Click the **Forms** directory to display all files, as shown in Figure 3-35.

![](img/840007e8f98ea6653e5877e945c27dc6_134_0.png)

### Figure 3-35 Viewing the contents of the Forms directory

- 5. To salvage the deleted file, follow these steps:
    - a. Click the **Info** icon in the first row of the NetWare File Listing table to display directory information (see Figure 3-36).

![](img/840007e8f98ea6653e5877e945c27dc6_134_1.png)

### Figure 3-36 Viewing directory information for the Forms directory

    - b. Click the **Select for list** link next to the Salvageable files text, and record the salvageable files here:
        - _____________
    - c. Click the **Salvage** option next to the Salvage.txt file to restore this file.
    - d. Click the **Back to directory page for** link and then the **Back to directory listing** link to return to the NetWare File Listing window.
    - e. Click your **Forms** directory and verify that the Salvage.txt file has been restored.
- 6. To delete the **Junk.txt** file, follow these steps.
    - a. Click the **Info** icon to the left of the Junk.txt file and record the file name, size, and deleter information for one deleted file:
        - ____________________________________________________________________
    - b. Scroll down and click the **Delete file** button, and then click **Yes** to delete the Junk.txt file.
- 7. Follow these steps to purge deleted files from the Forms directory:
    - a. Click the **Info** icon next to the Forms directory.
    - b. Click the **Select for list** link next to the Salvageable files text.
    - c. Click the **Purge all files** button.
    - d. Click the **Back** button on your browser to return to the Directory entry information window.
    - e. Record the salvageable files:
        - ____________________________________________________________________
- 8. Click **Exit** to return to the Remote Manager Login window.
- 9. Close your Web browser and return your computer to the standard lab configuration.

## CHAPTER SUMMARY

- The basic components of Novell Storage Services (NSS) include partitions, pools, volumes, directories, and files. Storage pools are made up of one or more physical disk partitions. The volume is the logical division of the storage pool and is comparable to a file cabinet drawer in that it holds folders and files. Each server is required to have a minimum of one NSS volume named SYS consisting of at least 4 GB.
- During installation, NetWare creates a number of system directories on the SYS volume, including the Login, Public, and System directories. The Login directory contains programs and files needed to log a user into the network. The Public directory contains program commands and utilities that may be run by a user after logging in to the network. The System directory contains OS files and utilities available only to the network administrator. It's important that the SYS volume doesn't run out of available space. Because running out of space on the SYS volume can bring down the server, network administrators usually plan one or more data volumes to contain the organization's files and applications.
- Files are used to store network data and software. In addition to file name and size, NetWare stores additional information about each file, including owner, access dates, and attributes in the directory entry table located at the beginning of each volume. Network administrators can use Remote Manager from a Web browser to manage the network file system.
- An important job of a network administrator is to plan and implement a structure for the network file system that supports the organization's processing needs. When planning the directory structure, Novell suggests setting aside private home directories for each user, shared directories to store files that multiple users need, and application directories. To provide space for these directories, many network administrators use multiple volumes. The SYS volume is reserved for OS files, and one or more data volumes are usually designated to store print queues, user files, and applications.
- After a directory structure has been designed, any necessary volumes are created in ConsoleOne or Remote Manager.
- After all volumes are created and mounted, a network administrator can create the necessary directories and subdirectories by using Windows Explorer, Linux Konqueror (file-management utility), ConsoleOne, or Remote Manager.

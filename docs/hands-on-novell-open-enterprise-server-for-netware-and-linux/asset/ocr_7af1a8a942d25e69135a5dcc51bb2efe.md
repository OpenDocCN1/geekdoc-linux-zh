+   7. Follow these steps to record permissions for the products directory:
+   a. Click the **products** directory and click **Properties** to open the Properties dialog box.
+   b. Click the **Permissions** tab and record the permissions: _______________________________
+   c. Close the products directory window.

8. Use the procedure in Step 7 to record permissions for the facilities directory:
________________________________________________________________

9. Close Konqueror, and leave your system running for the next activity.

# Sharing and Accessing Network Files

As with any server operating system, one of the major functions of a Linux server is sharing data with client computers. In Linux, you can share directories with other Linux and UNIX systems by using the standard **Network File System (NFS)**. You can also share data with a Windows client by using the Samba service described in Chapter 14. In this section, you learn how to use NFS to share files on your Linux server.

Novell OES has NFS configured and ready to go. All you have to do is use YaST to start the service and add the directories you want shared on the network. To use YaST to enable NFS, use the following steps:

+   1. Start YaST and, if necessary, enter your root user password.
+   2. Click **Network Services** in the left pane to display the menu options. You can select NFS Client or NFS Server options. The NFS Server option is used to share directories, and the NFS Client option is used to mount remote directories.
+   3. To share a directory, click the **NFS Server** option in the right pane to open the Configuration of the NFS server dialog box.
+   4. Click the **Start NFS server** option button, and then click **Next** to display the *Directories to export to the others* dialog box (see Figure 13-30).

![](bbox=[0.1, 0.61, 0.85, 0.88])

+   5. Click the **Add directory** Button and then use the **Browse** button to navigate to the EngData directory and then to the directory you want to share.
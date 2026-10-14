Add a directory to the list by selecting **Add**. The dialog in Figure 13-6 appears.

![](bbox=[0.098, 0.105, 0.659, 0.253])

**Figure 13-6**

From this dialog, you can configure the directory to mount in your file system tree. Configure the directory by doing the following:

+   1. In the NFS Server Hostname field, enter the NFS server’s hostname, or find and select the NFS server from a list of NFS servers on your network by selecting Choose.
+   2. In the Remote File System field, enter the *exported directory* on the NFS server you want to mount, or find and select the available directory by selecting Select.
+   3. In the Mount Point (local) field, enter the *mount point* in your local file system tree to mount the exported directory, or browse to and select the mount point by selecting Browse.
+   4. In the Options field, enter any *options* you would normally use with the mount command. For a list of these options, enter `man mount`.
+   5. When you have completed configuring the directory, select OK. You are returned to the NFS Client Configuration dialog.

Save the NFS client settings by selecting Finish. The settings are saved in /etc/fstab, services are restarted, and the exported directories are mounted in your local file system tree.

![](bbox=[0.018, 0.619, 0.205, 0.689])

# Exercise 13-1: Import Network File System (NFS)

In this exercise, create an /import/sled10 directory and use it as a mount point to import the /export/sled10 directory from da1 using NFS. Create an /etc/fstab entry to mount the directory automatically at boot time.

You can use the command-line interface or YaST to do this. The following step-by-step description uses YaST.

# Detailed Steps to Complete This Exercise

To add a remote file system to the NFS client, do the following:

+   1. Open a terminal window and su – to root (password n0v311).
+   2. Create a mount point named /import/sled10 for the remote file system to be mounted on your computer by entering

```
mkdir -p /import/sled10
```
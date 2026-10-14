# Detailed Steps to Complete This Exercise

To create a AutoYaST control file, do the following:

+   1. In a terminal window, run the su -- command to switch to root (password n0v311) and enter yast2.
+   2. In the YaST Control Center, select Miscellaneous > Autoinstallation.
+   3. Select Tools > Create Reference Profile; select Create.
+   4. Browse through the created profile by selecting sections of the tree on the left side of the dialog and selecting entries in the main window. Change the configuration if you like.
+   5. Save the file by selecting File > Save, enter sled10.xml as the filename, and select Save.
+   6. Have a look at the file /var/lib/autoinstall/repository/sled10.xml in a text editor. Quit the editor when done.
+   7. Close any open windows.

# Objective 4—Installation Server: Setup and Use

An installation server offers the files needed for the installation of SUSE Linux Enterprise Desktop via the network. To provide such a server in your network, you need to understand how to:

+   - Set Up an Installation Server
+   - Use the Installation Server

# Set Up an Installation Server

The installation repository requires a certain layout of directories and files on the installation server. The most convenient way to set up such an installation repository is to use SUSE Linux Enterprise Server 10 and its YaST module Installation Server. This module creates the necessary directory structure, prompts you to insert the CDs or DVD to copy their content to the proper directories, and sets up the server (NFS, HTTP, FTP) used to distribute the files. You can also use SUSE Linux Enterprise Desktop 10 as an installation server. However, there is no YaST module for this purpose, so you have to set up the server manually. The following steps are required:

+   - Fill the Installation Repository
+   - Configure the NFS Server

# Fill the Installation Repository

First create a directory, such as /export/sled10, where you want to store the installation repository using the mkdir -p /export/sled10 command. Filling the repository is very simple: Just insert the SUSE Linux Enterprise Desktop 10 Installation DVD and copy all files on it to the repository:

```
cp -a /media/SLED100.001/* /export/sled10/
```
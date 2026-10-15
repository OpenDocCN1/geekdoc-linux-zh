![](bbox=[0.07, 0.12, 0.59, 0.48])

Figure 14.14 DOSIdle helps prevent the DOS virtual machine from monopolizing your CPU's attention.

5. That's all! You should run DOSIdle every time you use the virtual machine and suspect you might want to multitask in Linux or another virtual machine. Therefore, you might want to add the line c:\dosidle\dosidle to the bottom of your autoexec.bat file.

Because DOS has no VMware Tools, you cannot directly shrink a DOS virtual disk. You can, however, mount the DOS virtual drive in a Windows or Linux virtual machine and initiate the shrink from there.

# Networking in DOS: Tricky, but Possible

If you have the patience to install the AMD PCNet Family packet driver, you're about halfway to exploiting the virtual Ethernet card in VMware. Now you need a networking program to run. You may have noticed I have a fondness for FTP, so why would I stop now?

This is how you download, install, and test an FTP program from DOS:

+   1. Download the Wattcp FTP program from ftp://ftp.oldskool.org/pub/tvdog/internet/ftp07.zip
+   2. Transfer the ftp07.zip archive to the DOS virtual machine via floppy or virtual disk mount.
+   3. Unzip the archive into a new directory, c:\ftp.
+   4. Before you can run any Internet programs, you need to configure your IP address. Unfortunately, using dynamic address schemes such as a DHCP is difficult to do manually using most DOS Internet clients. You have to do it yourself no matter what. The IP configuration file for this FTP program is
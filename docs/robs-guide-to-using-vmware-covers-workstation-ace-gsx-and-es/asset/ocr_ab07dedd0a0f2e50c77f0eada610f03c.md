1. Start out with node one powered on and node two powered off.

2. In node one, open the Computer Management via the Administrative tasks menu item and select Disk Management.

Note: If the Write Signature and Upgrade Disk Wizard runs, then do not convert your new disk to a dynamic disk. If it is converted to a dynamic disk, then right-click the disk in Disk Management and select Revert to Basic Disk.

3. Right-click the Unallocated disk space on your new disk and create a new primary partition. The minimum size for your quorum disk must be 50 Mb. If you have created a 100 Mb or a 500 Mb disk, you should use the entire disk at this point. Format it as NTFS and assign it a drive letter. Q: is a commonly used letter for the Quorum disk.

![](bbox=[0.1, 0.51, 0.88, 0.85])

Figure 29.1: The Quorum disk is configured in the first node as drive Q:.

4. At this point, it is important to verify that you can access the disk. Add a text file to the newly created Quorum disk and enter some information in the file.
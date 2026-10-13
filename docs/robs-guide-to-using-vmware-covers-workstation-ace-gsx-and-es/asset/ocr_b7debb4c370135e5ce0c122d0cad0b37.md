29. Power off the two nodes and add a Fixed Sized SCSI disk to both node one and node two. Do not forget to click Allocate disk space now. Make sure it is configured on SCSI bus 1 just as it is on your quorum disk. For example, if your quorum disk is SCSI 1:0, configure your new disk as SCSI 1:1.

After adding your disk, your configuration should look like the one in Figure 24.12.

![](bbox=[0.15, 0.28, 0.97, 0.68])

Figure 24.12: Add a second SCSI disk to the Windows cluster for shared data.

Tip: If you forget to specify the disk for channel 1, you can always click the Advanced button (see Figure 24.12) to change the disk to SCSI 1:1.

30. First power on node one.

31. Open Disk Management in Computer Management and format the disk and assign a drive letter.

32. Next, we are going to create a new group in Cluster Administrator. Click Groups in the left panel and select New → Group.
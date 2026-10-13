+   7. Select the driver and return to the Device Driver screen. Both the Storage adapter and the SCSI hard disk are now listed. If you select continue, the drivers will be loaded.
+   
+   8. Select continue on the remaining screens and HTDETECT will be unloaded.

# Prepare for Cluster Services installation

When you are adding the drivers to prepare your servers for Cluster Services installation, perform the steps described in this chapter on both servers.

When the drivers are loaded on both servers, issue the `list devices` command on the two servers and make sure that both servers show the extra disk that was added. The following image shows the shared SCSI-disk which was added to both servers.

![](bbox=[0.07, 0.46, 0.75, 0.62])

Figure 14.8
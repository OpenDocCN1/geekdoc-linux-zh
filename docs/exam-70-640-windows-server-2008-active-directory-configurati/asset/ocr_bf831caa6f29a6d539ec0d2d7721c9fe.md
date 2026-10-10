# CONFIGURE SCHEDULED ACTIVE DIRECTORY BACKUPS

**GET READY.** To perform this exercise you must be logged into the server as a member of the Administrators group. To perform this backup, you must have a second hard drive volume available that is at least 1 MB larger than the critical volumes of the server that you are backing up. These steps assume that you are backing up to a local volume. You must also have the Window Server Backup feature installed on the Windows Server 2008 computer; this can be installed from the Server Manager console if you have not done so already.

+   1.  Log on to the domain controller as the default Administrator or a member of the Backup Operators group. On the Start menu, click **Administrative Tools** and select **Windows Server Backup**. The Windows Server Backup window is displayed.
+   2.  In the right pane, select **Backup Operators**. The Getting Started window is displayed.
+   3.  Click **Next**. The Specify Backup Type window is displayed.
+   4.  If you are backing up to a local device, select **Custom** and click **Next**. The Select Backup Items window is displayed.
+   5.  Verify that the destination volume has not been selected and click **Next**. The Specify backup time window is displayed, as shown in Figure 11-9.

![](bbox=[0.11, 0.39, 0.75, 0.69])

+   6.  Select the time that you want the backups to take place and click **Next**. The Select Destination Disk window is displayed.
+   7.  If your backup destination disk does not appear automatically, click **Show All Available Disks**, place a checkmark next to the destination, and click **OK**.
+   8.  Place a checkmark next to the desired destination disk and click **Next**. A Windows Server Backup warning is displayed, as shown in Figure 11-10.

![](bbox=[0.11, 0.83, 0.75, 0.97])
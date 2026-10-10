+   9. To change the default path of the FTP home directory, click the **User** tab and enter **CORP\Shared\Download** in the Default home directory text box.

+   10. To have all users access the default home directory rather than their home directories, click to select the **Always use ‘Default home directory’** instead of the user’s home directory from eDirectory check box.

+   11. To allow the public to download files from the Shared\Download directory, you need to enable anonymous access to the FTP server. To do this, scroll down to the Anonymous Users section, shown in Figure 11-17.

![](bbox=[0.09, 0.22, 0.62, 0.45])

Figure 11-17 Enabling the Anonymous user account

+   12. Click the **Allow** check box, and then enter the path to the CORP\Shared\Download directory in the Anonymous user directory text box.

+   13. Click the **Save** button and then click **OK** in the success message box to return to the User tab.

+   14. Follow these steps to stop and then restart the FTP service:
+   a. If necessary, click the **FTP** link under the File Protocols heading to display the main FTP Server Administration window.
+   b. Click the **Stop** button to stop the service.
+   c. Click the **Start** button to restart the FTP service.

+   15. After the FTP server status changes to **Running**, click the **Exit** button to end your iManager session.

+   16. Follow these steps on your Windows XP computer to modify the Ftprest.txt file in the SYS\ETC directory:
+   a. Map drive letter F: to the SYS volume by clicking **Start, Run**, typing **MAP F:=SYS:**, and pressing **Enter**.
+   b. Start Notepad. Click **File, Open** from the menu, and open the F:\Etc\Ftprest.txt file.
+   c. Make the modifications shown previously in Figure 11-16.
+   d. Save the file and exit Notepad.

+   17. Close all open windows, and stay logged in for the next activity.

# Accessing FTP Folders and Files

After FTP Server is up and running, you can use any FTP client to log in to the FTP server and transfer files. In the following activity, you use an FTP client to access the classroom FTP server and issue several commands.
3. Start your Web browser, enter the URL: **https://IPaddress/iFolder** (replacing *IPaddress* with the IP address assigned to your iFolder server), and then press **Enter**. (Using "https" encrypts data transmissions by using a secure port, thus increasing security.)

+   4. Click the **Login** option under the *Access your Files* heading, and, if necessary, click **Yes** to proceed with the security certificate. If requested, enter Eric's passphrase used for encryption.
+   5. Enter Eric's user name and password, and then click **OK** to log in and display the NetStorage window.
+   6. Click the **iFolder** directory to expand it, and record the file names:
+   7. Click to select the check box for the file you copied in Activity 10-8.
+   8. Click the **File** link and then click **Download**, and download the file to your desktop.
+   9. Minimize your Web browser.
+   10. Start a text editor such as WordPad, and open the file you copied to your desktop in Step 8. Add the following line of text:
+       mm/dd/yy Room 129.00
+   11. Save the file with a new name, and exit the text editor.
+   12. Follow these steps to upload the updated file:
+       a. Maximize your Web browser.
+       b. Click the **iFolder** directory, click the **File** link, and then click the **Upload** button to open the Novell Upload File dialog box.
+       c. Check the **browse** button to select the file you saved in Step 11, and then click **Upload** to start the upload process. The new file should then appear in your iFolder directory.
+   13. Click the **Logout** option to exit your session, and close your Web browser.
+   14. Follow these steps to use your Windows system to access your iFolder data:
+       a. If necessary, start Windows and log in to the directory with the Ekenton user name and password.
+       b. Log in to iFolder as **Ekenton**. Double-click his iFolder home directory, and open the file you uploaded in Step 12.
+   15. Close any open windows, and log out. Leave your system running for the next activity.

![](bbox=[0.15, 0.62, 0.72, 0.69])

# INSTALLING AND USING NETDRIVE

Although NetStorage enables users to view, upload, and download their iFolder and network data from any client, it doesn't provide direct access to data from applications by using standard drive mappings. Novell has made provisions for creating network drive mappings by using HTTP via NetDrive. With **NetDrive**, you can map a network drive to any NetWare 6.5 OES server without using Novell Client. In addition, because NetDrive uses HTTP, you can map the drive from your Internet-connected system. The main disadvantage of using NetDrive compared to NetStorage is that NetDrive requires installing a small client on the local computer. If you're working from a computer where you don't have rights to install the NetDrive client, such as at an airport kiosk or in a hotel room, you can still use NetStorage to access your files online. In the following sections, you learn how to install and use NetDrive to create drive mappings from a Web browser.
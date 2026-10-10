# Activity 11-5: Working with FTP Services

Time Required: 10 minutes

Objective: Use Web Manager to configure FTP Server.

Requirements: Installation of FTP Server on a dedicated or classroom server. If you're using a dedicated server, you need to have completed Activities 11-3 and 11-4. This activity should be performed on a Windows XP computer.

Description: After configuring the Web server, Eric informed Kellie Thiele that the site was ready to use. Kellie logged in to the FTP server and transferred some files to the Download directory. In this activity, you use an FTP client to log in to your FTP server with the KThiele account and carry out some FTP activities, including creating a directory and transferring files. You then log in as an anonymous user and download a file.

+   1. If necessary, start your computer, and log in to the Novell network with your administrative user name and password.
+   2. Use Notepad to create the following text file named ##Readme.txt (replace ## with your assigned student number) in the root of your C: drive:

```
Date: today's date
Created by: your name
This file contains instructions on installing the latest updates to the station thruster control software.
```

+   3. Exit Notepad and save your file.
+   4. To open an FTP client window, click Start, Run and enter FTP IPaddress (replacing IPaddress with the IP address of your server). Then press Enter to display the “User IPaddress:(none)” login prompt.
+   5. Enter the distinguished name for KThiele and press Enter to display the Password prompt.
+   6. Enter password and press Enter to display a message stating that KThiele logged in successfully.
+   7. Enter ? and press Enter to display a list of FTP commands.
+   8. Enter the Put C:\##\readme.txt command and press Enter to send your file to the FTP server.
+   9. Enter Bye and press Enter to exit the FTP client and return to your Windows desktop.
+   10. Start your Web browser and enter the URL ftp://IPaddress (replacing IPaddress with the IP address of your server) to display the Login As window.
+   11. Click the Log on anonymously check box, and then click the Log on button to display a window showing all files in the FTP site. (If you can't log in anonymously, log in with your eDirectory administrative user name and password.)
+   12. Open another student's file by double-clicking it. Read the file and then close the window.
+   13. If necessary, use My Computer to create a Downloads folder at the root of your C: drive.
+   14. Download a file to your computer. Right-click the file name, and then click Copy to folder to open the Browse for Folder dialog box.
+   15. Navigate to your C: drive, and click the Downloads folder. Click OK to download the file.
+   16. Log out by exiting the Web browser.
+   17. Verify that the file has been downloaded by using My Computer to navigate to your Downloads folder, and double-click the new file.
+   18. Close all windows, and log out. Leave your system running for the next activity.

- d. Click **OK** to create the LinuxUsers group and display the completion message.
- e. Click **OK** to display the Enable Group for LUM window.
- f. Click the **Object Selector** button next to the Select the Linux Config object text box, and then click the **UNIX Config** object.
- g. Click **OK** to display the completion message, and then click **OK** again to return to the iManager main window.

6. Follow these steps to create a user account named LUMUser:
    - a. Scroll down, click to expand the **Users** heading if necessary, and then click the **Create User** link.
    - b. Enter **LUMUser** in the Username text box and **LinuxUser** in the Last name text box.
    - c. Click the **Object Selector** button next to the Context text box, click the **Users OU**, and then click **OK**.
    - d. Enter a password in the Password and Retype Password text boxes.
    - e. Click **OK** to create the LUMUser account, and then click **OK** again to return to the iManager main window.

7. Follow these steps to enable the LUMUser account for Linux:
    - a. Under the eDirectory Administration heading, click the **Modify Object** link.
    - b. Click the **Object Selector** button next to the Object name text box, navigate to the **Users OU**, and click the **LinuxUsers** group.
    - c. Click **OK** to display the Modify Object: LinuxUsers.Users.UAS group window, and click the **Members** tab.
    - d. Click the **Object Selector** button next to the Members text box, and then click the LUMUser account.
    - e. Click **OK** to return to the Members window, and then click **OK** again to save your changes and return to the iManager main window.

8. Follow the procedure in Step 6 to create a user account named **RegUser** but don’t make it Linux-enabled.

9. Exit iManager, and log out.

## NetWare Core Protocol (NCP) Services in SUSE Linux

As shown in Figure 14-3, the NCP service enables the SUSE Linux server to process requests from Novell clients. Windows computers running Novell Client can log in to the Linux server and access NSS volumes and NCP-enabled directories as though they were on a NetWare server. The default OES installation creates an NCP-enabled directory named sys in the /usr/novell directory that acts like the SYS volume on a NetWare server. This NCP-enabled sys directory contains Login and Public subdirectories to hold files that are available to all users. When a user logs in from Novell Client, the F: drive is mapped to the NCP-enabled sys directory, and the Z: drive is mapped to the Public subdirectory.

The NCP service and its directory shares are managed in the Novell Remote Manager utility. Figure 14-4 shows an example of the Manage Shares options in this utility. In the following activity, you create a Linux directory and then use Novell Remote Manager to share the directory as an NCP volume.

### Planning and Implementing Novell OES on Linux

![](img/840007e8f98ea6653e5877e945c27dc6_581_0.png)

Figure 14-3 Using the NCP service in SUSE Linux

![](img/840007e8f98ea6653e5877e945c27dc6_581_1.png)

Figure 14-4 NCP configuration options

### Activity 14-3: Creating an NCP-Enabled Directory

**Time Required:** 10 minutes

**Objective:** Use Novell Remote Manager to configure NCP services.

**Requirements:** Access to the SUSE Linux server with your administrative account, completion of Activity 14-2, and a Windows XP computer with Novell Client installed.

**Description:** To complete the test environment Eric asked you to create, in this activity you use Novell Remote Manager to view NCP options and then create a Linux directory and share it as an NCP volume.

1. If necessary, start your Windows XP computer and log in to eDirectory with the **RegUser** account you created in Activity 14-2.

2. Open My Computer and record the network drive letters and their associated paths:

3. Open the **SYS** volume and record the directories:
   ....................................................
   ....................................................

4. Log off your Windows XP computer.

5. If necessary, log in to your SUSE Linux server with the **root** user name and password.

6. Follow these steps to create a directory named **NCPTest** on your SUSE Linux server:
    - a. Open a terminal session.
    - b. Type the following commands, pressing **Enter** after each one:
      ```
      cd /
      mkdir NCPTest
      ```
    - c. Type **exit** and press **Enter** to end your terminal session.

7. From your SUSE Linux server, start a Java-enabled browser, and start Novell Remote Manager by entering **https://IPAddress:8009** (replacing *IPAddress* with the IP address of your SUSE Linux server).

8. Log in to Novell Remote Manager with your administrative user name and password.

9. To view NCP server information, under the **Manage NCP Services** heading, click the **View Server Information** link. Record the following information:

   | Item | Value |
   | :--- | :--- |
   | Server name | ......................................... |
   | NCP requests | ......................................... |
   | Open files | ......................................... |

10. Follow these steps to make the NCPTest directory an NCP share:
    - a. Under the **Manage NCP Services** heading, click the **Manage Shares** link.
    - b. Scroll down and click the **Create new share** button.
    - c. Enter **NCPData** in the **Share Name** text box, and click **OK** to display the **Path** text box.
    - d. Enter */NCPTest* in the **Path** text box, and click **OK** to display the summary window.
    - e. Click **OK** again to confirm the settings and return to the Novell Remote Manager main window.

11. Exit Novell Remote Manager.

12. Start iManager by entering the URL **https://IPAddress/nps/iManager.html** replacing *IPAddress* with the IP address of your SUSE Linux server.

13. Log in to iManager with your eDirectory user name and password.

14. Follow these steps to create a login script for the Users OU that maps the N: drive to the NCPTest directory:
    - a. Under the eDirectory **Administration** heading, click the **Modify Object** link.
    - b. Click the **Object Selector** button next to the **Object** name text box, click the **Users OU**, and then click **OK** to display the **Modify Object: Users: UAS** window.
    - c. Click the **Login Script** link.
    - d. Enter the **MAP ROOT N:=NCPTest:** login script command.
    - e. Click **OK** to save your changes and return to the iManager main window.

15. Exit iManager.

![](img/840007e8f98ea6653e5877e945c27dc6_582_0.png)

The following steps require using a Windows XP computer.

16. If necessary, start your Windows XP computer and log in to eDirectory with your administrative user name and password.

17. Follow these steps in Windows Explorer to make the Users OU a trustee of the NCPTest directory with all rights except Supervisor and Access Control:
    - a. Open My Network Places, and double-click the **Novell Connections** option.
    - b. Double-click your SUSE Linux server to display all the NCP volumes.
    - c. Right-click the **NCPTest** volume and click **Trustee Rights** to display the NetWare Services dialog box.
    - d. Click the **Users OU**, and then click **Add** to add the Users OU to the Trustees list box.
    - e. Click to select all the rights check boxes except the A check box.
    - f. Click **OK** to save your trustee assignment.

18. Close all windows, and log off your Windows XP computer.

### Activity 14-4: Testing NCP Access

**Time Required:** 10 minutes

**Objective:** Use NCP to access network files through a drive mapping.

**Requirements:** Completion of Activity 14-3.

**Description:** In this activity, you complete the test environment Eric asked you to create by logging in as the test user and then verifying drive mappings.

1. If necessary, start your Windows XP computer, and log in to eDirectory with the **RegUser** account you created in Activity 14-2.

2. Use My Computer to check your drive mappings. Record the drive mappings here: ___________________

3. Start Notepad and create a simple text file containing your name and a short message.

4. Save the file as **message.txt** on your N: drive.

5. Log out.

6. Log in to eDirectory with your **LUMUser** name and password.

7. Use My Computer to check your drive mappings. Do you have an N: drive? ____________________

8. If you have an N: drive, open the **message.txt** file and make a change.

9. Save the file, exit Notepad, and then log out.

10. Log in to your SUSE Linux server with the root user name and password, and open a terminal session.

11. Use the following commands (pressing **Enter** after each command) to change to your NCPTest directory and view its contents:
    ```
    cd /NCPTest
    ls -l
    cat message.txt
    ```

12. Record your results: ___________________

13. Close your terminal session and log out. Leave your system running for the next activity.

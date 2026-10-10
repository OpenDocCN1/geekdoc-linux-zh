![](bbox=[0.12, 0.07, 0.68, 0.35])

# Activity 10-8: Using NetStorage to Access Files

**Time Required:** 10 minutes

**Objective:** Access files by using NetStorage.

**Requirements:** If you’re using a dedicated server, you need to complete Activity 10-6 to install NetStorage on your NetWare server. If you’re using a shared classroom server, NetStorage must be installed by your instructor. You also need a Forms directory in your CORP data area and Read and File Scan rights to all users. This activity can be performed on a Windows XP or SUSE Linux 10 computer.

**Description:** After installing NetStorage on the UASHOST server, Eric tested the system by logging in to the NetStorage server with his EKenton user name and then verified access to his files and folders. In this activity, you log in to the NetStorage server and practice accessing your files and folders.

+   1. If necessary, log on to your local computer. (If the Novell iFolder Login window is displayed, click **Cancel** to bypass the iFolder login.)

+   2. Follow these steps to add a drive mapping to EKenton’s login script:
+   
+   a. Start **iManager** and log in with your administrative user name and password.
+   
+   b. Click to expand the **Users** heading and then click the **Modify User** link.
+   
+   c. Click the **Object Selector** button, navigate to your **IT OU**, and then click the **EKenton** user name.
+   
+   d. Click **OK** to display information for the EKenton user.
+   
+   e. Click the **Login Script** link on the General tab options to display the Login script window.
+   
+   f. Enter `MAP M:=UASHOST\CORP:\Forms` if you’re using a dedicated server or `MAP M:=UASHOST\STUDENTS:\##CORP\Forms` if you’re using a classroom server (substituting your assigned student number for `##`).
+   
+   g. Click **OK** to save the login script command.
+   
+   h. Exit **iManager**.

+   3. Start your Web browser, enter the URL `http://IPAddress/NetStorage`, and press **Enter**. (Replace *IPAddress* with the IP address assigned to your NetWare 6.5 server.) Be careful when you enter the URL because it’s case sensitive.
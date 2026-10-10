d. Click **OK** to save your changes and return to the **Printer (Non NDPS)** dialog box.

e. Click **OK** to return to the NetWare Administrator browse window.

5. If you're continuing to the next activity, leave NetWare Administrator open and stay logged in. If not, exit NetWare Administrator, and log out.

# Activity 8-3: Creating a Print Server Object

![](bbox=[0.03, 0.18, 0.09, 0.24])

**Time Required:** 10 minutes

**Objective:** Set up a queue-based printing system.

**Requirements:** Same as Activity 8-1

**Description:** For queue-based printing to work, the print server software needs to know what printers it controls and who the print server operators and users are. This information is supplied when you create and configure an eDirectory print server object. In this activity, you create a print server object for the **UAS** container and then configure it to manage the **IT_P** printer.

+   1.  If necessary, log in to eDirectory with your administrative user name and password, start NetWare Administrator, and open a browse window to the UAS container.

+   2.  Follow these steps to create a print server object in your UAS container:
+       a.  Click the **UAS** container, if necessary, and press **Insert** to open the New Object dialog box.
+       b.  Scroll down and double-click the **Print Server (Non NDPS)** object to open the Create Print Server dialog box.
+       c.  Enter **UAS_PS** in the Print Server name text box, and click the **Define additional properties** check box.
+       d.  Click the **Create** button to create the print server object and open the Printer (Non NDPS) dialog box.

+   3.  Follow these steps to assign your printer to the new print server:
+       a.  Click the **Assignments** button, and then click the **Add** button to open the Select Object dialog box.
+       b.  Double-click the **IT OU** in the Browse context section to display the printer in the Available objects section.
+       c.  Double-click the **IT_P** printer in the Available objects section.

+   4.  Follow these steps to document the default users and operators of the print server and make the **ITMgrs** group a print server operator:
+       a.  Click the **Users** button, and record the users of the print server here: _______________________
+       b.  Click the **Operator** button, and record the name of the print queue operator here: _______________________
+       c.  Click the **Add** button to open the Select Object dialog box, and then double-click the **IT OU** in the Browse context section.
+       d.  Double-click the **ITMgrs** group in the Available objects section.

+   5.  Click **OK** to save your print server configuration and return to NetWare Administrator.

+   6.  Exit NetWare Administrator. If you're continuing to the next activity, stay logged in. If not, log out.
+   - Add drivers from the workstation you are running Novell iManager from by selecting **Add** from System.
+     The drivers installed on your workstation are made available for upload to the Driver Store.
+     You can upload only drivers for the same platform as the workstation.

+   4. Select the driver you want; then select **OK**.
+   5. Save your changes by selecting **OK**.

![](bbox=[0.113, 0.242, 0.304, 0.319])

You can also install driver files from a terminal prompt using the `iprntcmd` command.
For details, see “Using iprntcmd on Linux and Macintosh,” on page 37 in the Novell OES iPrint Administration Guide for Linux.
You can access the guide from http://www.novell.com/documentation/oes or from the OES_Docs directory on your 3086 Course DVD 2.

# ## Create a DNS Name for the Print Manager

The Print Manager creates a URL for each printer based on the Print Manager configuration.
When you create the Print Manager, you can specify an IP address or DNS name for the Novell iPrint Service.
You should always use a DNS name because using an IP address forces users to delete and reinstall printers if the IP address changes.

# ## Set Up and Configure the Print Manager

The Print Manager provides a platform where Printer Agents can reside on the server. Printer Agents are representations of actual printers. When a print job is submitted to the Print Manager, the print job is forwarded to a printer when the printer is ready.
To set up and configure the Print Manager, do the following:

+   - Create a Print Manager
+   - Start the Print Manager

# ### Create a Print Manager

You need to create at least one Print Manager for your print system; depending on your network setup, you can create additional Print Managers (for example, across a WAN link).
The Print Manager must be running to create printers.
A Driver Store must exist before you create a Print Manager.
To create a Print Manager, do the following:

+   1. Make sure you have configured a DNS name for the Print Manager.
+   2. From Novell iManager (on the left), select **iPrint > Create Print Manager**.
+   3. Fill in the appropriate fields.
+      To view explanations about the fields, select Help.
+   4. Make sure the **Start Print Manager after Creation** check box is selected.
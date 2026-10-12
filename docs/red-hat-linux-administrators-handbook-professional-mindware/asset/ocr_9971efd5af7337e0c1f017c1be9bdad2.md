+   3. Scroll down the module list and locate the module you want to deactivate. Toggle the This module is active check box so that the module becomes inactive.
+   4. Click the **Accept** button.
+   5. If you have nothing else to do in Linuxconf, click the **Quit** button. You are prompted to activate the changes. Click **Activate** the changes to complete the process.

The next time you run Linuxconf, it will tell you that it is removing the menu items related to the inactive module.

# Defining user privileges

Linuxconf also allows you to create privileged user accounts that can be used to administer a certain aspect of your Linux system. This feature should be a great help if you have coadministrators in your organization. Perhaps you want to offload some of the simpler administrative tasks to junior administrators. In such a case, you can create normal user accounts with restricted sets of privileges. Suppose you have a normal user account called kabir and want to assign some administrative privileges to this account. Do the following:

+   1. Run linuxconf from your root account.
+   2. Select Config User accounts Normal User accounts from the Linuxconf screen. A list of all normal users on your system appears.
+   3. Locate the target user (kabir in this example) and double-click the line of the user's record. You will see a screen similar to the one shown in Figure 4-8.
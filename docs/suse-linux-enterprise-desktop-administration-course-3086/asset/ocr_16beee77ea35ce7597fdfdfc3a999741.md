![](bbox=[0.094, 0.068, 0.281, 0.138])

For more information on login scripts, see “Running Novell Login Scripts During Login.”

7. (Optional) To configure integrated login, select the **Startup** tab, make sure **Run Novell Client Login at Session Startup** is selected (it is selected by default), and then select **Save profile after successful login**.

You must have the User Name and Password fields and the Tree and Context fields on the eDirectory tab filled out for this to be saved, and you must save your profile in order for an integrated login to happen at the next session startup.

8. To log in to the server you specified in Step 3, select **OK**.

# Running Novell Login Scripts During Login

When you successfully log in to the network, one or more login scripts are executed. Login scripts can be used to automatically map drives and search drives to directories, display messages, set environment variables, and execute programs or menus.

You can specify whether login scripts are run, whether the results are displayed, and whether the login window is automatically closed during login. In addition, if the login script uses the %2, %3, %4, or %5 variable, you can set these variables by clicking the Variables button.

Your network administrator should provide information on whether to use login scripts and, if so, which login scripts to use.

![](bbox=[0.094, 0.508, 0.281, 0.579])

For additional information on setting up login scripts, see the *Novell Login Scripts Guide* available at http://www.novell.com/documentation/linux_client/pdfdoc/login.pdf and on the 3086 Course DVD 2 in the OESDocs directory.

# Logging Out of a Network Location (Server or Tree)

You can log out of a network location in either of the following ways:

+   - To log out of all existing connections, select [menu icon] > Novell Logout > Logout.
+   - If you are logged in to multiple trees and want to log out of a specific server or tree, select [menu icon] > Novell Connections, select the tree or server that you want to log out of, and then select Detach.
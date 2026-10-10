+   1. If necessary, start your computer and log on to your local Windows computer with your assigned Windows administrator user name and password.
+   2. If you're using a classroom server, follow these steps to map a drive to the network directory containing the Novell Client files:
+      a. Click **Start, Run** and then enter `\\IPaddress` (substituting the IP address of your classroom server).
+      b. In the login window, enter your assigned user name and password.
+      c. Navigate to the **SYS** volume and open the **Public** directory.
+      d. Navigate to the **NovellClient** folder and click the **SETUPNW.exe** program.
+      e. Skip to Step 4.
+   3. If you're using a dedicated server, insert the Novell Client CD in the CD-ROM drive. If the Novell Client installation doesn't start automatically, use Windows Explorer to open the CD-ROM drive, and then double-click **SETUPNW.exe** to start the Novell Client Installation Wizard.
+   4. Click the client installation option for your Windows version.
+   5. Read the license information, and then click the **Yes** button to accept the license agreement.
+   6. Verify that the Typical Installation option button is selected, and then click the **Install** button.
+   7. After the installation is finished, click the **Reboot** button to restart your computer.
+   8. When the computer restarts, the Novell Login window should be displayed. Do not log in at this time. In the next section, you customize Novell Client and use it to practice logging in to your eDirectory tree.

# ## Logging in with Novell Client

Before accessing resources or services on a network, users must first authenticate themselves by providing a valid user name and password to the client software. The client software then uses the user name and password to authenticate the user to the network. Novell refers to the process of using Novell Client to authenticate a user as **logging in** to the network. To access the local Windows computer, Microsoft also requires the user to authenticate by using a valid user name and password. Microsoft refers to this authentication process as **logging on** to the computer. As a result, when you access the Novell network from a Windows system, you need to perform two authentication processes. First, you log in to the eDirectory tree using Novell Client. Novell Client then attempts to log on to the local Windows computer with the local user name specified in the Windows tab and the password you supplied to Novell Client. If your local Windows computer has a user account with the specified local user name and password, you are automatically logged on to the local computer; if not, you see a Windows logon window and must then enter a valid user name and password to authenticate to the local computer before proceeding.

To allow users to access the Novell network, the network administrator needs to create a user account in Novell's eDirectory for each user. To make accessing the local computer easier, the network administrator can also create a user account on the Windows computer with the same user name and password as the Novell user name. Because Novell's eDirectory service stores user accounts in containers arranged in a tree structure, users must supply their context along with their user names and passwords when logging in. Figure 4-25 shows the Novell Login window after clicking the Advanced button. Notice that the window contains text boxes for Username, Password, Tree, Context, and Server.

By default, the Username text box contains the name and context of the last user who logged in from your computer. If no one has logged in since the client was installed, the Username text box is blank. The Password text box is where you enter the password for your user account. This field is kept blank to prevent someone else from logging in as the previous user. Your password is used like a signature, allowing the eDirectory service to verify that you're the actual user of the account.

The Context text box is used to specify the path leading to the container where your user name is stored. You can use the buttons to the right of each text box to browse for a tree, container, or server instead of typing in the object's exact name (see Figure 4-26). The list arrows next to each text box enable you to select from previously used trees and contexts.
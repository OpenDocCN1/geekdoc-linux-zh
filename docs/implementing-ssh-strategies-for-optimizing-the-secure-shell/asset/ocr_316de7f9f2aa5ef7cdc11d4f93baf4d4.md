![](bbox=[0.13, 0.09, 0.6, 0.39])

**Figure 5.8** User Access Control screen of VShell's SSH server.

The VShell User Access Control screen (see Figure 5.8) shows two separate sections: the *Name* section and the *Permissions* section. The Name section is the section where the user names the operating system that needs to be set. The *Permissions* section sets the different types of permission that will be allowed to each user, including Logon, Shell, Remote Execution, SFTP, Port Forwarding, and Remote Port Forwarding.

Let’s say you want to grant access to the SSH server for the Backup group, to back up files on the SSH server. The Backup group is called Backup Operators and will need SFTP access but will not need shell access to the SSH server (as shown in Figure 5.9). Complete the following steps to add the appropriate connection filters:

+   1.  Select the Add button.
+   2.  Scroll down on the Windows Select User or Group menu and choose the Backup Operations group.
+   3.  Select the checkbox in the Allow column for the SFTP row.
+   4.  Select the checkbox in the Allow column for the Remote Execution row.
+   5.  Select the checkbox in the Deny column for the Shell row.
+   6.  Now the Backup Operators group has full SFTP access to the SSH server but does not have shell access to the server.
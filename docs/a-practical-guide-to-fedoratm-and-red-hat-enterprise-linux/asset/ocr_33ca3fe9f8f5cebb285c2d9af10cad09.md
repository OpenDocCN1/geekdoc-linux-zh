![](bbox=[0.41, 0.1, 0.69, 0.31])

> Add or modify Samba users

machines. Change the description of the server if you like. Click the **Security** tab and make sure **Authentication Mode** is set to **User**; you do not need to specify an Authentication Server or a Kerberos Realm. If you are using Windows 98 or later, set **Encrypt Passwords to Yes.** When you specify a username in the Guest Account, anyone logging in on the Samba server as **guest** maps to that user's ID. Click **OK**.

Select **menubar: Preferences→Samba Users** to display the Samba Users window (Figure 23-3). If the user you want to log in as is not listed in this window, click **Add User.** When you have the proper permissions, the Create New Samba User window displays a combo box labeled **Unix Username** that allows you to select a Linux user; otherwise, your username is displayed as the Unix Username. The Windows Username is the Windows username that you want to map to the specified Linux (UNIX) username. The Samba Password is the password this user or Windows enters to gain access to the Samba server.

If Sam's username is **sam** on both the Linux and Windows systems, you would select **sam** from the Unix Username combo box and enter **sam** in the Windows Username text box. If his username were **sls** under Linux and **sam** under Windows, you would select **sls** from the Unix Username combo box and enter **sam** in the Windows Username text box. Finally you would enter Sam's Windows password in the two Samba Password text boxes. Click **OK** to close the Create New Samba User window, then click **OK** to close the Samba Users window.

> User map

If you are mapping a Windows username to a *different* Linux username, you must add the following **username map** (page 843) parameter to the **[global]** section of /etc/samba/smb.conf (page 839):

```
username map = /etc/samba/smbusers
```

Without this line in smb.conf, Samba will not consult the user map file.

> Linux shares

Next you need to add a **share**, which is the directory hierarchy you export from the server (Linux) system to the client (Windows) system. Click the plus sign (+) on the toolbar to display the Basic tab of the Create Samba Share window (Figure 23-4). In
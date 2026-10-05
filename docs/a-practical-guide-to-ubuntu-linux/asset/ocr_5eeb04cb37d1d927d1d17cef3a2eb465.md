# SETTING UP A SAMBA SERVER 801

![](bbox=[0.281, 0.096, 0.843, 0.258])

**Figure 23-1** Samba Server Configuration window

Select Menubar: Preferences→Server Settings to display the Server Settings Windows tab (Figure 23-2). Change the workgroup to the one in use on the Windows machines. Change the description of the server if you like. Click the Security tab and make sure Authentication Mode is set to User; you do not need to specify an Authentication Server or a Kerberos Realm. If you are using Windows 98 or later, set Encrypt Passwords to Yes. When you specify a username in the Guest Account, anyone logging in to the Samba server as guest maps to the UID of the Linux user named nobody. Click OK.

**Samba users** Select Menubar: Preferences→Samba Users to display the Samba Users window (Figure 23-3, next page). If the user want to log in as is not already specified in this window, click **Add User**. When you have the proper permissions, Create New Samba User window displays a combo box labeled **Unix Username** that allows you to select a Linux user; otherwise, your username is displayed as the Unixname. The Windows Username is the Windows username that you want to map to the specified Linux (UNIX) username. The Samba Password is the password with this user or Windows enters to access the Samba server.

![](bbox=[0.386, 0.65, 0.735, 0.863])

**Figure 23-2** Server Settings window, Basic tab
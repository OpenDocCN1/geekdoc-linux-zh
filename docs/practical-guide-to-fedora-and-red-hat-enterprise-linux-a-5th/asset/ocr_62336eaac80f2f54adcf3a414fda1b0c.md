![](bbox=[0.43, 0.09, 0.65, 0.25])

Figure 23-2 Server Settings window, Basic tab

later, set Encrypt Passwords to Yes. When you specify a username in the Guest Account, anyone logging in on the Samba server as guest maps to that user's ID. Typically the guest account maps to the UID of the Linux user named nobody. Click OK.

Select Menubar: Preferences\Samba Users to display the Samba Users window (Figure 23-3). If the user wants to log in as is not already specified in this window, click Add User. When you have the proper permissions, the Create New Samba User window displays a combo box next to Unix Username that allows you to select a Linux user; otherwise, your username is displayed as the Unix Username. The Windows Username is the Windows username that you want to map to the specified Linux (UNIX) username. The Samba Password is the password this user or Windows enters to gain access to the Samba server.

If Zach has accounts named zach on both the Windows and Linux systems, you would select zach from the Unix Username combo box, enter zach in the Windows Username text box, and enter Zach's Windows password in the two Samba Password text boxes. Click OK to close the Create New Samba User window and click OK to close the Samba Users window.

# Adding a Samba password for the Linux user nobody

Because the user nobody exists in smbusers when you install Samba, you cannot add the user nobody. nor can you add a password for nobody from system-config-samba. Instead, you must use smbpasswd from the command line as follows:

```
# smbpasswd -a nobody
New SMB password:
Retype new SMB password:
```

Normally the user nobody does not have a password because it is the guest login. Press RETURN (without typing any characters) in response to each of the SMB password prompts to add nobody to the Samba password file without a password.

Next you need to add a share, which is the directory hierarchy that you export from the Linux system to the Windows system. Click the plus sign (+) on the toolbar to display the Basic tab in the Create Samba Share window (Figure 23-4). In the Directory text box, enter the absolute pathname of the directory you want to share (/tmp is an easy directory to practice with). Enter a description if you like. It can be useful
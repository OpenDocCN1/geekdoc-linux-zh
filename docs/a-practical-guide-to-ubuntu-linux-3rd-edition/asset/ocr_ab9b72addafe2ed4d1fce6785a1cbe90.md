![](bbox=[0.39, 0.09, 0.75, 0.31])

**Figure 23-4** Create Samba Share window, Basic tab

or whether you want to allow anyone to access this share. Click **OK**. Close the Samba Server Configuration window.

You should now be able to access the share from a Windows machine (page 814). There is no need to restart the Samba server.

Working with **root** privileges, you can use **smbpasswd** to change a Linux user's Samba password.

```
$ sudo smbpasswd sam
New SMB password: 
Retype new SMB password:
```

This example assumes Sam was a user on the Linux system before Samba was installed. When you install Samba, it copies all Linux users to the list of Samba users. If you add a user after you install Samba, you need to use the **-a** option to instruct **smbpasswd** to add the user to the list of Samba users. The following command adds a new Linux user, Max, to the list of Samba users and assigns a Samba password to Max:

```
$ sudo smbpasswd -a max
New SMB password: 
Retype new SMB password: 
Added user max.
```

Once a user has a Samba password, he can use **smbpasswd** without any arguments to change his password.

If a user has different usernames on the Linux and Windows systems, you must map the Windows username to a Linux username (see **username map** on page 811). Make sure all Linux users who will log in using Samba have Samba passwords.

You should now be able to access the new shares from a Windows machine (page 814). There is no need to restart the Samba server.
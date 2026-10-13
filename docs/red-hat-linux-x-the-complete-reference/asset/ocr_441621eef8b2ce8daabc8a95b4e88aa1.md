# Adding and Changing Passwords

At this point, /etc/samba/smbpasswd will contain entries for all your current users with dummy fields for the passwords. You then use the smbpasswd command to add, or later change, encrypted passwords. To add a password for a particular user, you use the smbpasswd command with the username:

```
# smbpasswd dylan
```

```
New SMB Password: new-password
Repeat New SMB Password: new-password
```

Users can use smbpasswd to change their own password. The following example shows how you would use smbpasswd to change your Samba password. If the user has no Samba password, they can just press the ENTER key.

```
$ smbpasswd
```

```
Old SMB password: old-password
New SMB Password: new-password
Repeat New SMB Password: new-password
```

# Configuring Encrypted Passwords

You also have to make sure that Samba is configured to use encrypted passwords. Set the encrypt passwords option to yes and specify the SMB password file. These options are already set in the /etc/samba/smb.conf file (described in the following section), but they are commented with a preceding ; symbol. Just locate the lines and remove the ; symbols at the beginnings of the lines:

```
encrypt passwords = yes
smb passwd file = /etc/samba/smbpasswd
```

You can also use SWAT to make this change. In the GLOBALS page, select Yes from the pop-up menu for the Encrypt Password entry. Then save your changes by clicking the Commit Changes button.

Be sure to restart the Samba server with the following command:

```
service smb restart
```
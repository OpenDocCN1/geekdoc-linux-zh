# The Samba User Database

You could set up identical usernames and passwords for both the Microsoft Windows and Samba-enabled Linux computers on a network. However, this is not always possible, especially when there are preexisting databases. In that case, you can set up a database of Samba users and passwords that correspond to current Microsoft usernames and passwords on your network. A template is available in /etc/samba/smbusers and is in effect if you add the following entry to the smb.conf file:

```
username map = /etc/samba/smbusers
```

If you're comfortable with the command line interface, the quickest way to set up Samba users is with the smbpasswd command. Remember that you can create a new Samba user only from valid accounts on a Linux computer.

However, you can configure such an account without login privileges on the Linux system. For example, the following command adds the noted user without a valid login shell:

```
# useradd winuser1 -s /sbin/nologin
```

You can then configure that user with a Samba password with the smbpasswd -a winuser1 command. The smbpasswd command is powerful; it includes a number of useful switches described in Table 15.4.

TABLE 15.4
| smbpasswd Switch | Description |
|---|---|
| -a username | Adds the specified username to the database. |
| -d username | Disables the specified username; thus disables that password from Microsoft networking. |
| -e username | Enables the specified username; opposite of -d. |
| -r computername | Allows changes to a Windows or Samba password on a remote computer. Normally goes with -U. |
| -U username | Normally changes the username on a remote computer, if specified with the -r switch. |
| -x username | Deletes the specified username from the database. |
The [homes] section allows each user to be able to access his or her Linux home directory from a Windows system on the LAN. The user will be able to write to the home directory. However, other users will not be able see or share this directory. The [printers] section allows all users to print to any printer that is configured on the local Linux system.

# Adding Samba users

Doing user-style Samba security means assigning a Linux user account to each person using the Linux file systems and printers from his or her Windows workstation. (You could assign users to a guest account instead, but in this example, all users have their own accounts.) Then you need to add SMB passwords for each user. For example, here is how you would add a user whose Windows 98 workstation login is chuckp:

+   1.  Type the following as root user from a Terminal window to add a Linux user account:

```
# useradd -m chuckp
```

+   2.  Add a Linux password for the new user as follows:

```
# passwd chuckp
Changing password for user chuckp
New UNIX password: ******
Retype new UNIX password: ******
```

+   3.  Repeat the previous steps to add user accounts for all users from Windows workstations on your LAN that you want to give access to your Linux system to.

+   4.  Type the following command to create the Samba password file (smbpasswd):

```
# cat /etc/passwd | /usr/bin/mksmbpasswd.sh > /etc/samba/smbpasswd
```

+   5.  Add an SMB password for the user as follows:

```
# smbpasswd chuckp
New SMB password: ******
Retype new SMB password: ******
```

Repeat this step for each user. Later, each user can log in to Linux and rerun the passwd and smbpasswd commands to set private passwords.

# Starting the Samba service

To start the Samba SMB and NMB daemons, you can run the /etc/init.d/smb start-up script by typing the following as the root user:

```
# /etc/init.d/smb start
```

This runs the Samba service during the current session. To set up Samba to start automatically when your Linux system starts, type the following:

```
# chkconfig smb on
```
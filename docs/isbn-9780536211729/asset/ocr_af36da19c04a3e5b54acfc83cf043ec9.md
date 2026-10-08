but they will prevent symlink attacks that could be done by a user linking /etc/passwd into their home directories, and then copying it off of the machine. If you allow users to have shell access to the machine along with Samba access, you may wish to set these directives to false:

```
admin users
hosts equiv
smbpasswd
use hosts
username map
```

These directives can be used to play tricks with user permissions. The admin directives allow a user or group of users to assume root privileges in the context of a share. Hosts equiv and use rohosts allows a computer to bypass password checking. Smb-password and username map, if not watched, could point to a manufactured file, where all of the passwords were blank or where the user account associations were disturbed.

# # 3.8.6 The smbpasswd File

The smbpasswd file is required if you wish to use encrypted passwords on your Windows computers, which is the default since Windows 95 OSR-2 and Windows NT, patch level 3. You will need to have the directive

```
encrypt passwords = yes
```

in the smb.conf file.

The smbpasswd file consists of 6 different colon-delimited fields:

+   1. User name. This is an unencrypted Windows username. Case is not important.
2. UNIX ID. This is the UID to control file system permissions. If Billy logs into the Windows box, this is the UID of Billy's account on the Linux box.
3. LAN manager password. The user's password is used as salt against a determined character sequence to derive this entry.
4. NT-password. The password is converted to Unicode and then encrypted using MD4.
5. Account flags. This tells you which type of account is being used.
6. The time from UNIX epoch when the last account update occurred.

```
U = user account
D = disabled
N = an account with no password
W = a workstation account used to configure Samba's Domain controller features.
```

If you have the null passwords directive in the smb.conf file, you should not see any accounts without passwords. As a system administrator, watch very carefully for these. The following perl will help you find null accounts quickly:

```
#!/usr/bin/perl -T -w
```
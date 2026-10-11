When SELinux is set to use a targeted policy, Samba is protected by SELinux. You can disable this protection if necessary. For more information refer to “Setting the Targeted Policy with system-config-selinux” on page 416.

Under Samba, an exported directory hierarchy is called a share.

The name Samba is derived from SMB (page 1106), the protocol that is the native method of file and printer sharing for Windows.

# Samba Users, User Maps, and Passwords

For a Windows user to gain access to Samba services on a Linux system, the user must provide a Windows username and a Samba password. In some cases, Windows supplies the username and password for you. It is also possible to authenticate using other methods. For example, Samba can use LDAP (page 1090) or PAM (page 458) instead of the default password file. Refer to the Samba documentation for more information on authentication methods.

The supplied username must be the same as a Linux username or must map to a Linux username. Samba keeps the username maps in /etc/samba/smbusers. Users with the same username on Linux and Samba do not need to appear in this file, but they still need a Samba password.

When you install Samba, smbusers has two entries:

```
```bash
$ cat /etc/samba/smbusers
# Unix_name = SMB_name1 SMB_name2 ...
root = administrator admin
nobody = guest pcguest
dog
```
```

The first entry maps the two Windows usernames (administrator and admin) to the Linux username root. The second entry maps three Windows usernames, including guest, to the Linux username nobody: When a Windows user attempts to log in on the Samba server as guest, Samba authenticates the Linux user named nobody.

Samba uses Samba passwords—not Linux passwords—to authenticate users. By default, Samba keeps passwords in /etc/samba/smbpasswd. As Samba is installed, authentication for root or nobody would fail because Samba is installed without passwords: The smbpasswd file does not exist.

Each of the configuration techniques described in this chapter allows you to add users to smbusers and passwords to smbpasswd. You can always use smbpasswd as discussed later in this section to add and change passwords in smbpasswd.

When you attempt to connect from Windows to a Samba server, Windows presents your Windows username and password to Samba. If your Windows username is the same as or maps to your Linux username, and if your Windows and Samba passwords are the same, you do not have to enter a username or password to connect to the Samba server.

You can add the following line to smbusers to map the Windows username sam to the Linux username sls:

```
sls = sam
```
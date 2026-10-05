# Chapter 30 Cooperating with Windows

outside your organization to prevent your users from accidentally down-loading files in the clear across the Internet. Blocking is typically implemented at the network firewall level; Samba uses UDP ports 137 through 139 and TCP ports 137, 139, and 445.

Since the release of Samba version 3, excellent documentation has been available on-line from samba.org.

Samba comes with sensible defaults for its configuration options, and most sites will need only a small configuration file. Use the testparam -v to get a listing of all the Samba configuration options and the values to which they are currently set. This listing includes settings from the smb.conf file as well as any default values you have overridden.

Avoid setting options in the smb.conf file unless they are different from the default values and you have a clear idea of why you want to lock them. The advantage of this approach is that your configuration automatically adapts to the settings recommended by the Samba authors when you upgrade to a newer version of Samba.

That having been said, make sure that password encryption is turned on:

```
encrypt passwords = true
```

This option encrypts the password exchange between Windows clients and the Samba server. It's currently the default, and there's no conceivable situation in which you would want to turn it off.

The encryption feature requires the Samba server to store a Windows password hash for every user. Windows passwords work in a fundamentally different way from UNIX passwords, and therefore it is not possible to use the passwords from /etc/shadow.

Samba provides a special tool, smpasswd, for setting up these passwords. For example, let's add the user tobi and set a password for him:

```
$ sudo smpasswd -a tobi
New SMB password: password
Retype new SMB password: password
```

Users can change their own Samba passwords with smpasswd as well:

```
$ smpasswd -r smbserver -U tobi
New SMB password: password
Retype new SMB password: password
```

This example changes the Samba user of tobi on the server smbserver.

Windows passes the current user's credentials to the Samba server when establishing a connection. For this reason, users' Samba passwords are usually set to match their Windows passwords.
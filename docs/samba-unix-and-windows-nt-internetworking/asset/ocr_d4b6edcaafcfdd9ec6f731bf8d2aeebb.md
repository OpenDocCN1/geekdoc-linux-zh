```
Rename: "New Value #1" to
"EnablePlainTextPassword", dword:00000001
```

# Encrypted Passwords

It is possible to eliminate the clear-text password option during SMB session setup by enabling NTLM encrypted password support in Samba. The feature improves overall network security by removing the possibility of password eavesdropping on the wire; however it increases the complexity of maintaining and synchronizing the UNIX and NTLM password spaces. Enabling encrypted passwords requires maintenance of an additional password file containing NTLM passwords. This must be done in conjunction with the standard UNIX password maintenance activities.

The NTLM encrypted password option is enabled by setting the encrypt passwords parameter to true. Before you turn on encrypted password support you need to create an instance of the Samba smbpasswd file that includes an entry for each of your users. Usually the easiest way to do this is by using your existing UNIX or NIS password file as input to the mksmbpasswd.sh shell script supplied in the Samba distribution. The procedure is described in Example 7.4.

```
encrypt passwords = <true, false>
```

# Example 7.4 Enabling Samba NTLM Encryption Support

```
$ cat /etc/passwd | mksmbpasswd.sh > \
/usr/local/samba/private/smbpasswd
$ chown -R root.root /usr/local/samba/private/smbpasswd
$ chmod 500 /usr/local/samba/private
$ chmod 600 /usr/local/samba/private/smbpasswd
```

Update smb.conf parameter.

```
encrypt passwords = true.
```

The smbpasswd file is stored in the /usr/local/samba/private directory by default. You can indicate an alternate location by specifying the directory path as a value to the smb passwd file parameter:

```
smb passwd file = <path>
```

The format of each entry in the smbpasswd file is listed in Table 7.2. In general, it is similar to standard UNIX password file format. Like its UNIX counterpart it uses a ":" to delimit each field. Take special note of the two fields that contain 32 "X" characters. These two fields are placeholders for the LAN Manager and NT versions of the hashed password respectively. It is crucial that the fields initially contain 32 "X" characters if they are to be recognized by smbd.

# Table 7.2 smbpasswd Format
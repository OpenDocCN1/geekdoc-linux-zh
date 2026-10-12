# Note

The documentation packaged with Red Hat 7 contains detailed discussions of plain versus encrypted passwords and their ramifications. See these documents:

+   /usr/share/doc/samba-2.0.7/docs/textdocs/Win95.txt
+   /usr/share/doc/samba-2.0.7/docs/textdocs/WinNT.txt
+   /usr/share/doc/samba-2.0.7/docs/textdocs/ENCRYPTION.txt

Windows NT users, please note that NT SMB clients present some additional challenges. Be sure to read these three documents carefully if you are having problems with Windows NT SMB clients.

For Windows 2000, be sure to see `http://us1.samba.org/samba/ftp/docs/Win2000_PlainPassword.reg`.

# Enabling Encrypted Passwords on the Server

In the `[global]` section, uncomment `encrypt passwords = yes`. Assuming the client username is `mryuid`, perform the following command:

```
# smbpasswd -a mryuid
```

# Note

The preceding command fails unless the SMB password file, `/etc/samba/smbpasswd`, exists. The easiest way to use the `touch` command is as follows:

```
# touch /etc/samba/smbpasswd
```

Note that in other Linux distributions, or in Samba implementations compiled from source, the location of `smbpasswd` may be different.

Type in the password. If the password is not the same as it is on the client, the user will be prompted for the password the first time he accesses the Samba server.

You can even enable or disable password encryption on a client-by-client basis. To do so, you need to make a small include file for each client. The config file must contain the client's netbios name in the filename, and must contain an `encrypt` parameter in the file. For instance, if there are two clients, `win98box` and `win95box`, and `win95box` does not use encryption, here's the proper `win98box.encrypt`:

```
encrypt passwords=no
```
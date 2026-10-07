**preferred master, domain master** These two parameters also affect whether Samba takes on master browser duties. If set to Yes, preferred master causes Samba to attempt to take on this role, which can be quite detrimental if the server isn't configured to win elections. Therefore, we recommend setting this value to No unless you understand the election process. Likewise, domain master determines whether Samba tries to become the domain master browser (as opposed to the local master browser, which is slightly different).

**hosts allow** This parameter is an important security feature. If used, it blocks Samba access to all but the specified computers. You can list computers by hostname (not the NetBIOS name, if they differ) or by IP address. If a hostname begins with a period, or if an IP address with fewer than four elements ends with a period, that signifies an entire network of computers. In the preceding example, for instance, all computers on the 192.168.34.0/24 network are allowed access. Although this parameter isn't necessary, it's a good idea to use it, particularly if the server is connected to the Internet at large.

The most critical of these parameters are workgroup and encrypt passwords. When you first install Samba, it's not likely to be configured to function on your workgroup, so chances are you *must* set the workgroup parameter to use the server. Likewise, unless you're using fairly old clients, you must normally either configure Samba to use encrypted passwords or reconfigure your clients to use cleartext passwords.

# ## Setting Password Options

If you set encrypt passwords = Yes, you must set up an encrypted password file on Linux. To do this, you can use the smbpasswd program, which adds a username and password to the encrypted password file (/etc/samba/smbpasswd on Red Hat 7.3 systems) or edits that information. For each user on your system, you should issue the command `smbpasswd -a`. The program will ask you to enter the password twice. The first time you run this program, it may notify you that it can't find the smbpasswd file, and so is creating it.

If you prefer to use cleartext passwords and the normal Linux password database, you can do so by changing any recent Windows clients to send cleartext passwords. On Red Hat 7.3 systems, the directory /usr/share/doc/samba-2.2.3a/docs/Registry contains several .reg files that can be used to make the appropriate changes to Windows systems. Copy the file named after the version of the OS you're running (such as Win98_PlainPassword.reg for Windows 98) to a floppy disk, move that disk to the target Windows system, and double-click the file to adjust the client's configuration. You'll need to reboot Windows before the changes will take effect.

# ## Configuring File Shares

File shares make up the bulk of most smb.conf files, particularly on servers that have many shares. This share demonstrates the most common file-sharing options:

```
```ini
[bigshare]
    comment = Shared Program Directory
    path = /home/samba/bigshare
    read only = No
    browseable = Yes
    create mask = 0666
    directory mask = 0777
```
```

The meanings of this share's parameters are as follows:
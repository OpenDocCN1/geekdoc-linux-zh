# Starting Up Samba

For a simple Samba setup, you should be able to use the default smb.conf file installed with the Linux distribution package of Samba. If you need to make changes, however, you must restart the Samba server to have the changes take effect. Starting, stopping, and restarting the Samba server is managed by the /etc/rc.d/init.d/smb script using the options start, stop, and restart. On Red Hat, you can run the smb script directly as shown here:

```
service smb restart
```

On Red Hat, you can also use the desktop Services configuration tool (redhat-config-services) to start and stop Samba.

To ensure name resolution, you can enter the name of your host and its IP address in the /etc/hosts file. On Windows systems, lmhosts entries consist of an IP address and the system's NetBIOS name, the name it is known by on a Microsoft network. For your Linux system, you can enter the IP address and the Linux system's hostname.

# Accessing Samba from Linux

To test your connection from a Linux system, you can use the smbclient command to query the Samba server. To access the home directory of a user on the Samba server, use the IP or hostname address of the Samba server, along with the homes section. With the -U option, specify a user to connect to on the system, as shown here:

```
smbclient //turtle.mytrek.com/homes -U dylan
```

You are then prompted for a password. If the client password is different from the server password, use the server password. Once connected, you are presented with the SMB client prompt as shown here. You can then access the files on the user's home directory:

```
smb: \>
```

# Accessing Samba from Windows

To set up a connection for a Windows client, you need to specify the Windows workgroup name and configure the password. The workgroup name is the name that appears in the Entire Network window in the Network Neighborhood on the Windows desktop (My Network Places on Windows 2000, NT, and XP). In the smb.conf file, you specify the workgroup name in the workgroup entry in the global section. The workgroup name should be uppercase, no more than eight characters, and contain no spaces.

You can then restart the Samba server. On a Windows client, you see the workgroup name in the Entire Network folder in your Network Neighborhood. Within the workgroup is an icon for the Samba server, and within that is an icon for the user directory, as specified in the homes section of the smb.conf file.

# Samba Configuration File and Tools

Samba configuration options are kept in the /etc/samba/smb.conf file. You edit this file to make changes to the configuration. Once you finish making any changes, you should test your smb.conf file using the testparm program. The testparm program checks the validity of your configuration entries. By default, testparm uses the /etc/samba/smb.conf file, although you can supply a different configuration file as an argument:

```
testparm
```

To check your network connections, use the smbstatus command. This command returns a listing of all active SMB connections.

Note The /etc/samba/smbusers file associates Windows network usernames with corresponding users on your Linux Samba server. For example, admin and administrator are made equivalent to the Linux root user.
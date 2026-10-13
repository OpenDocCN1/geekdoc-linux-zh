
- You already allow plain-text-based services, such as FTP and Telnet, between your Windows machine and Red Hat Linux server.
- Your network is not connected to the Internet, so use of plain-text passwords does not pose a great threat to your organization.
- You just want to get Samba working first and then deal with either encrypted passwords or plan on delegating all authentication tasks to a Windows NT Server in the long run.
- Use encrypted passwords for authentication.

You probably will choose the first option, so it is described next. The details of using encrypted passwords for authentication are provided in the last section of this chapter, “Securing Your Samba Server.”

If you are using Windows 98, Windows 95 with Service Pack 3 or higher, or Windows NT 4 with Service Pack 3 or higher, follow these steps to enable plain-text passwords:

- 1. Run the Windows Registry editor program called RegEdit.
- 2. For Windows 9x, locate the following Registry key:
```
/HKEY_LOCAL_MACHINE
/System
/CurrentControlSet
/Services
/VxD
/VNETSUP
```
For Windows NT 4 with Service Pack 3 or higher, locate the following Registry key:
```
/HKEY_LOCAL_MACHINE
/SYSTEM
/CurrentControlSet
/Services
/Rdr
/Parameters
```
- 3. After you locate the VNETSUP branch (for Windows 9x) or the Parameters branch (for Windows NT) in the Registry tree, select Edit→ New and choose to create a new DWORD value.
- 4. RegEdit will insert a new DWORD value called New Value #1 in the Registry. Rename this new value EnablePlainTextPassword and double-click this new name.
- 5. A dialog box pops up, enabling you to set a value for the EnablePlainTextPassword you just created. Enter 1 as the value and close RegEdit as usual.
- 6. Reboot your Windows 9x/NT system.

This ensures that your Windows 9x/NT system is able to use plain-text passwords for SMB authentication.

## socket options

By default, the socket options parameter in the global configuration section is set to TCP_NODELAY, which enhances Samba performance on certain platforms. You should leave this parameter as is.

## dns proxy

This parameter affects how the Samba suite's built-in Windows Internet Name Server (nmbd) behaves when a Windows system name (NetBIOS name) cannot be resolved to an IP address. If you set this parameter to yes, the nmbd server will treat the NetBIOS names as an Internet domain name and try to resolve it by using the DNS protocol. Keeping the default setting is recommended.

## Setting the [homes] parameters

The [homes] section is a special configuration section that allows you to set up home directory access from Windows systems. In other words, a user with a valid username/password on the Red Hat system can access her home directory on the Linux system from a Windows system. The default [homes] configuration is as follows:

```
[homes]
    comment = Home Directories
```
```
browseable = no
writable = yes
```

Here is how you can change these parameters.

- **comment.** Exactly what its name suggests. Set this to whatever you wish.
- **browseable.** Controls whether or not home directories are visible in a browser list (such as the Network Neighborhood) or when the NET VIEW command is used from the Windows command prompt. Set this to yes or no depending on your needs.
- **writable.** Controls whether or not a user can write to her own home directory. For most practical purposes, this needs to be set to yes. If you set this to no, a user will have read-only access to her own home directory.

## Setting the [printers] parameters

The [printers] section is useful only if you have one or more printers attached to your Red Hat Linux system. The default [printers] configuration is as follows:

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = yes
```

Here is how you can change these parameters.

- **comment.** Exactly what its name suggests. Set this to whatever you wish.
- **path.** Set this to the directory where printer data files will be spooled. If you have a lot of users, make sure you have plenty of disk space for this directory.
- **browseable.** By default, printers are not visible in a browser (such as Network Neighborhood) or NET VIEW command output. To change this behavior, set this to yes.
- **guest ok.** By default, printer services are not available to guest users who do not have passwords. To change this behavior, set this to yes.
- **printable.** By default, this parameter permits printing. If this is set to no, printing is completely disabled.

The default configuration includes many commented configuration parameters and additional sections. Carefully investigate these options and enable anything that you want to use. However, if you are using Samba for the first time, first get it working using the default configuration.

## Managing Samba via Web

Using the new Web based configuration tool, SWAT, shipped with Samba, you can manage the Samba using a standard Web browser. Here is how you can use SWAT.

- 1. Verify that your `/etc/services` file has the following line:
```
swat 901/tcp
```
If the above line is not present, add this line and save `/etc/services` file.
- 2. Verify that your `/etc/inetd.conf` file has the following line:
```
swat stream tcp nowait.400 root /usr/sbin/swat swat
```
If the above line is missing or commented out, add or uncomment it and save `/etc/inetd.conf` file. In such a case restart inetd daemon using `killall -HUP inetd` command.
- 3. Next, run your favorite Web browser which can access your Samba server. Enter the following URL:
```
http://your-samba-server:901/
```
- 4. You will be asked to enter a username and password. Enter root as the username and the corresponding password. If you have entered an appropriate username/password pair, you will see the SWAT welcome screen.
- 5. Click on the available links to manage various aspects of Samba.

If you plan to access SWAT from machines other than the Samba server itself, you should secure it as follows:

- 1. Edit /etc/inetd.conf such that you have the following line:
```
swat stream tcp nowait.400 root /usr/sbin/tcpd /usr/sbin/swat swat
```
- 2. Edit /etc/hosts.deny to have the following line:
```
swat: ALL
```
- 3. Next, edit /etc/hosts.allow to have a line such as the following:
```
swat: IP-address-of-machine
```
Here IP-address-of-machine is the IP address of the machine where you plan to run the Web browser that will access SWAT.

You can have multiple IP addresses listed as long as they are separated by at least a space character.

## Testing the /etc/smb.conf configuration

Any time you change a Samba configuration file, run the testparm utility that is bundled with the Samba package. When you run this nifty utility from the command line, it checks the syntax of the /etc/smb.conf file and gives you useful warning and error messages. Because a misconfigured /etc/smb.conf file can be a security hole, use this utility whenever you modify this file.

## Starting, stopping, and restarting the Samba service

After you make sure that your /etc/smb.conf file is error-free, you are ready to start Samba. Two daemons come with the Samba package. The smbd daemon is the Samba server, and the nmbd daemon is the NetBIOS name server. To start the daemons, run the following command as root:
```
/etc/rc.d/init.d/smb start
```
You can then start accessing the Samba server from your Windows computers. To stop the Samba server, run the same command with a stop argument. You can also restart the daemons by using the same command with a restart argument.

If you want to start the Samba service at boot time, create a symbolic link as follows:
```
ln -s /etc/rc.d/init.d/smb  /etc/rc.d/rc3.d/S91smb
```
This starts the Samba service when your Red Hat Linux server enters run level 3, which is the default run level for all multiuser systems.

If you use an X Window System-based login (using XDM) and want to start Samba automatically, create the following link:
```
ln -s /etc/rc.d/init.d/smb  /etc/rc.d/rc5.d/S91smb
```

## Using a Linux File Server on Windows

Using a Linux file server on Windows probably is the most common reason why a Linux administrator in a Linux/Windows shop may consider using Samba. For example, suppose you want to make a Linux partition (or directory) called /intranet available to a group of Windows users (john, mary, and phil) on your LAN. Here is what you do:

- 1. If you set the security parameter in the [global] configuration section to user or share, create three user accounts (john, mary, and phil) on your Linux system. These user accounts need to be set up such that the password for each account matches its Windows counterpart. For example, if jennifer's password on her Windows system is set to tsk#tsk, then you must set her Linux account with the same password. Also, create a group called intranet in /etc/group that includes users jennifer, chad, and phil as the only members.
- 2. Modify the /etc/smb.conf file to add the following:
```
[Intranet]
    comment = Intranet Directory
    path = /intranet
```

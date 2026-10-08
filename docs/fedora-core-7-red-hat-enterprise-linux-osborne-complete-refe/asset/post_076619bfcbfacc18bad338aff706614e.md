
## Testing the Samba Configuration

After you make your changes to the **smb.conf** file, you can then use the **testparm** program to see if the entries are correctly entered. **testparm** checks the syntax and validity of Samba entries. By default, **testparm** checks the **/etc/samba/smb.conf** file. If you are using a different file as your configuration file, you can specify it as an argument to **testparm**. You can also have **testparm** check to see if a particular host has access to the service set up by the configuration file.

With SWAT, the Status page will list your connections and shares. From the command line, you can use the **smbstatus** command to check on current Samba connections on your network.

To check the real-time operation of your Samba server, you can log in to a user account on the Linux system running the Samba server and connect to the server.

## Domain Logons

Samba also supports domain logons whereby a user can log on to the network. Logon scripts can be set up for individual users. To configure such netlogon capability, you need to set up a **netlogon** share in the **smb.conf** file. The following sample is taken from the original **smb.conf** file. This share holds the **netlogon** scripts—in this case, the **/var/lib/samba/netlogon** directory—which should not be writable but should be accessible by all users (Guest OK):

```
[netlogon]
 comment = Network Logon Service
 path = /var/lib/samba/netlogon
 guest ok = yes
 writable = no
 share modes = no
```

The Global section would have the following parameters enabled:

```
domain logons = yes
```

With netlogon, you can configure Samba as an authentication server for both Linux and Windows hosts. A Samba username and password need to be set up for each host. In the Global section of the **smb.conf** file, be sure to enable encrypted passwords, user-level security, and domain logons, as well as an operating system level of 33 or more:

```
[global]
 encrypt passwords = yes
 security = user
 domain logons = yes
 os level = 33
```

> **NOTE** You can also configure Samba to be a Primary Domain Controller (PDC) for Windows NT networks. As a PDC, Samba can handle domain logons, retrieve lists of users and groups, and provide user-level security.

## Accessing Samba Services with Clients

Client systems connected to the SMB network can access the shared services provided by the Samba server. Windows clients should be able to access shared directories and services automatically through the Network Neighborhood and the Entire Network icons on a Windows desktop. For Linux systems connected to the same network, Samba services can be accessed using the GNOME Nautilus file manager and KDE file manager, as well as special Samba client programs.

With the Samba **smbclient**, a command line client, a local Linux system can connect to a shared directory on the Samba server and transfer files, as well as run shell programs. Using the **mount** command with the `-t cifs` option, directories on the Samba server can be mounted to local directories on the Linux client. The **cifs** option invokes **mount.cifs** to mount the directory.

### Accessing Windows Samba Shares from GNOME

You can use Nautilus (the GNOME file manager) to access your Samba shares. You can open the My Computer icon and then the Network icon. This will display the icons for your network. The Windows Network icon will hold the Windows workgroups that your Windows hosts are part of. Opening up the Windows Network icon will list your Windows network groups, like **WORKGROUP**. Opening up the Windows group icon will list the hosts in that group. These will show host icons for shared Windows hosts. Clicking a host icon will list all the shared resources on it. The following steps access your Windows shares:

1. Click My Computer to open a window with a Network icon.
2. Click the Network icon to open a window with a Windows network icon.
3. Click the Windows network icon to list your Windows network groups, such as workgroup.
4. Click the workgroup icon to list all your Windows hosts.

Alternatively, you can start Nautilus in browser mode and enter the **smb:** protocol to display all the Samba and Windows networks, from which you can access the Samba and Windows shares.

### smbclient

The **smbclient** utility operates like FTP to access systems using the SMB protocols. Whereas with an FTP client you can access other FTP servers or Unix systems, with **smbclient** you can access SMB-shared services, either on the Samba server or on Windows systems. Many **smbclient** commands are similar to FTP, such as **mget** to transfer a file or **del** to delete a file. The **smbclient** program has several options for querying a remote system, as well as connecting to it. See the **smbclient** Man page for a complete list of options and commands. The **smbclient** program takes as its argument a server name and the service you want to access on that server. A double slash precedes the server name, and a single slash separates it from the service. The service can be any shared resource, such as a directory or a printer. The server name is its NetBIOS name, which may or may not be the same as its IP name. For example, to specify the **myreports** shared directory on the server named **turtle.mytrek.com**, use //turtle.mytrek.com/myreports. If you must specify a pathname, use backslashes for Windows files and forward slashes for Unix/Linux files:
`//server-name/service`

You can also supply the password for accessing the service. Enter it as an argument following the service name. If you do not supply the password, you are prompted to enter it.

### Accessing Shares with smbclient

You can then add several options to access shares, such as the remote username or the list of services available. With the -I option, you can specify the system using its IP address. You use the -U option and a login name for the remote login name you want to use on the remote system. Attach % with the password if a password is required. With the -L option, you can obtain a list of the services provided on a server, such as shared directories or printers. The following command will list the shares available on the host **turtle.mytrek.com**:

```
smbclient -L turtle.mytrek.com
```

To access a particular directory on a remote system, enter the directory as an argument to the **smbclient** command, followed by any options. For Windows files, you use backslashes for the pathnames, and for Unix/Linux files, you use forward slashes. Once connected, an SMB prompt is displayed and you can use smbclient commands such as **get** and **put** to transfer files. The **quit** or **exit** commands quit the smbclient program. In the following example, smbclient accesses the directory **myreports** on the **turtle.mytrek.com** system, using the **dylan** login name:

```
smbclient //turtle.mytrek.com/myreports -I 192.168.0.1 -U dylan
```

In most cases, you can simply use the server name to reference the server, as shown here:

```
smbclient //turtle.mytrek.com/myreports -U dylan
```

If you are accessing the home directory of a particular account on the Samba server, you can simply specify the **homes** service. In the next example, the user accesses the home directory of the **aleina** account on the Samba server, after being prompted to enter that account's password:

```
smbclient //turtle.mytrek.com/homes -U aleina
```

You can also use smbclient to access shared resources located on Windows clients. Specify the computer name of the Windows client along with its shared folder. In the next example, the user accesses the **windata** folder on the Windows client named **lizard**. The folder is configured to allow access by anyone, so the user just presses the ENTER key at the password prompt.

```
$ smbclient //lizard/windata
```

Once logged in, you can execute smbclient commands to manage files and change directories. Shell commands can be executed with the ! operator. To transfer files, you can use the **mget** and **mput** commands, much as they are used in the FTP program.

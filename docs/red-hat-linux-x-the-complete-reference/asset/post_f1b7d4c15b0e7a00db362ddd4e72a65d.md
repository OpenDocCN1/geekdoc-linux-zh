
## Variable Substitutions

For string values assigned to parameters, you can incorporate substitution operators. This provides greater flexibility in designating values that may be context-dependent, such as usernames. For example, suppose a service needs to use a separate directory for each user who logs in. The path for such directories could be specified using the %u variable that substitutes in the name of the current user. The string path = /tmp/%u would become path = /tmp/justin for the justin user and /tmp/dylan for the dylan user. Table 37-3 lists some of the more common substitution variables.

Table 37-3: Samba Substitution Variables

| Variable | Description |
|---|---|
| %S | Name of the current service |
| %P | Root directory of the current service |
| %u | Username of the current user |
| %H | Home directory of the user |
| %h | Internet hostname on which Samba is running |
| %m | NetBIOS name of the client machine |
| %L | NetBIOS name of the server |
| %M | Internet name of the client machine |
| %I | IP address of the client machine |

## Testing the Samba Configuration

After you make your changes to the `smb.conf` file, you can then use the testparm program to see if the entries are correctly entered. testparm checks the syntax and validity of Samba entries. By default, testparm checks the `/etc/samba/smb.conf` file. If you are using a different file as your configuration file, you can specify it as an argument to testparm. You can also have testparm check to see if a particular host has access to the service set up by the configuration file.

With SWAT, the Status page will list your connections and shares. From the command line, you can use the `smbstatus` command to check on current Samba connections on your network.

To check the real-time operation of your Samba server, you can log into a user account on the Linux system running the Samba server and connect to the server.

## Domain Logons

Samba also supports domain logons whereby a user can log on to the network. Logon scripts can be set up for individual users. To configure such netlogon capability, you need to set up a netlogon share in the smb.conf file. The following sample is taken from the original smb.conf file. This share holds the netlogon scripts in this case, the /home/netlogon directory-which should not be writable but should be accessible by all users (Guest OK):

```
[netlogon]
comment = Network Logon Service
path = /home/netlogon
guest ok = yes
writeable = no
share modes = no
```

The Global section would have the following parameters enabled:

```
domain logons = yes
```

With netlogon, you can configure Samba as an authentication server for both Linux and Windows hosts. A Samba username and password need to be set up for each host. In the Global section of the smb.conf file, be sure to enable encrypted passwords, user-level security, and domain logons, as well as an operating system level of 33 or more:

```
[global]
encrypt passwords = yes
security = user
domain logons = yes
os level = 33
```

**Note** You can also configure Samba to be a Primary Domain Controller (PDC) for Windows NT networks. As a PDC, Samba can handle domain logons, retrieve lists of users and groups, and provide user-level security.

## Accessing Samba Services with Clients

Client systems connected to the SMB network can access the shared services provided by the Samba server. Windows clients should be able to access shared directories and services automatically through the Network Neighborhood and the Entire Network icons on a Windows desktop. For other Linux systems connected to the same network, Samba services can be accessed using special Samba client programs. With smbclient, a local Linux system can connect to a shared directory on the Samba server and transfer files, as well as run shell programs. With smbmount, directories on the Samba server can be mounted to local directories on the Linux client.

Note Several Samba browser clients are available for GNOME and KDE. For KDE, you can use Konba2 (downloadable from apps.kde.com). For GNOME, you can use Gnomba.

### smbclient

The smbclient utility operates like FTP to access systems using the SMB protocols. Whereas with an FTP client you can access other FTP servers or Unix systems, with smbclient you can access SMB-shared services, either on the Samba server or on Windows systems. Many smbclient commands are similar to FTP, such as mget, to transfer a file or del, to delete a file. The smbclient program has several options for querying a remote system, as well as connecting to it. See the smbclient Man page for a complete list of options and commands. The smbclient program takes as its argument a server name and the service you want to access on that server. A double slash precedes the server name, and a single slash separates it from the service. The service can be any shared resource, such as a directory or a printer. The server name is its NetBIOS name, which may or may not be the same as its IP name. For example, to specify the myreports shared directory on the server named turtle.mytrek.com, use //turtle.mytrek.com/myreports. If you must specify a pathname, use backslashes for Windows files and forward slashes for Unix/Linux files:

```
//server-name/service
```

You can also supply the password for accessing the service. Enter it as an argument following the service name. If you do not supply the password, you are prompted to enter it.

Note You can also use Nautilus (GNOME file manager) to access Samba shares. Use the smb: protocol, as in smb://lizard/windata. Entering just smb: will display all Samba shares.

### Accessing Shares with smbclient

You can then add several options to access shares, such as the remote username or the list of services available. With the -I option, you can specify the system using its IP address. You use the -U option and a login name for the remote login name you want to use on the remote system. Attach % with the password if a password is required. With the -L option, you can obtain a list of the services provided on a server, such as shared directories or printers. The following command will list the shares available on the host turtle.mytrek.com:

```
smbclient -L turtle.mytrek.com
```

To access a particular directory on a remote system, enter the directory as an argument to the smbclient command, followed by any options. For Windows files, you use backslashes for the pathnames, and for Unix/Linux files you use forward slashes. Once connected, an smb prompt is displayed and you can use smbclient commands such as get and put to transfer files. The quit or exit commands quit the smbclient program. In the following example, smbclient accesses the directory myreports on the turtle.mytrek.com system, using the dylan login name:

```
smbclient //turtle.mytrek.com/myreports -I 192.168.0.1 -U dylan
```

In most cases, you can simply use the server name to reference the server, as shown here:

```
smbclient //turtle.mytrek.com/myreports -U dylan
```

If you are accessing the home directory of a particular account on the Samba server, you can simply specify the homes service. In the next example, the user accesses the home directory of the aleina account on the Samba server, after being prompted to enter that account's password:

```
smbclient //turtle.mytrek.com/homes -U aleina
```

You can also use smbclient to access shared resources located on Windows clients. Specify the computer name of the Windows client along with its shared folder. In the next example, the user accesses the windata folder on the Windows client named lizard. The folder is configured to allow access by anyone, so the user just presses the ENTER key at the password prompt.

```
$ smbclient //lizard/windata
added interface ip=192.168.0.2 bcast=192.168.0.255 nmask=255.255.255.0
Got a positive name query response from 192.168.0.3 ( 192.168.0.3 )
Password:
Domain=[WORKGROUP] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
smb: \> ls
. D 0 Sat Sep 7 17:29:19 2002
.. D 0 Sat Sep 7 17:29:19 2002
hi A 10 Sat Sep 7 17:29:27 2002
mynewdoc.doc A 0 Sat Sep 7 16:59:13 2002
39997 blocks of size 1048576. 39930 blocks available
smb: \> mget hi
Get file hi? y
getting file hi of size 10 as hi (1.22069 kb/s) (average 1.2207 kb/s)
smb: \> quit
```

### smbclient Commands

Once logged in, you can execute smbclient commands to manage files and change directories. Shell commands can be executed with the ! operator. To transfer files, you can use the mget and mput commands, much as they are used in the FTP program. The recurse command enables you to turn on recursion to copy whole subdirectories at a time. You can use file-matching operators, referred to here as masks, to select a certain collection of files. The file-matching (mask) operators are *, [], and ? (see Chapter 8). The default mask is *, which matches everything. The following example uses mget to copy all files with a .c suffix, as in myprog.c:

```
smb> mget *.c
```

During transfers, you can have smbclient either prompt you for each individual file or simply transfer all the selected ones. The prompt command toggles this file prompting on and off.

To access a particular printer on a remote system, enter the printer name as an argument to the smbclient command, followed by any options. In the following example, smbclient accesses the myepson printer on the turtle.mytrek.com system, using the dylan login name:

```
smbclient //turtle.mytrek.com/myepson -U dylan
```

Once connected, an SMB prompt is displayed and you can use smbclient commands such as print to print files and printmode to specify graphics or text. In the next example, the user prints a file called myfile, after having accessed the myepson printer on turtle.mytrek.com:

```
smb> print myfile
```

### smbmount

With the smbmount command, a Linux or Unix client can mount a shared directory onto its local system. The syntax for the smbmount command is similar to that for the smbclient command, with many

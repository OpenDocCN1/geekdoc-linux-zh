
### Table 39-1 Samba Applications

| Application | Description |
|---|---|
| smbd | Samba server daemon that provides file and printer services to SMB clients |
| nmbd | Samba daemon that provides NetBIOS name resolution and service browser support |
| smbclient | Provides FTP-like access by Linux clients to Samba services |
| mount.cifs | Mounts Samba share directories on Linux clients (used by the **mount** command with the -t **cifs** option) |
| smbpasswd | Changes SMB-encrypted passwords on Samba servers |
| smbstatus | Displays the current status of the SMB network connections |
| smbrun | Interface program between **smbd** and external programs |
| testparm | Tests the Samba configuration file, **smb.conf** |
| smbtar | Backs up SMB/CIFS-shared resources directly to a Unix tape drive |
| nmblookup | Maps the NetBIOS name of a Windows PC to its IP address |
| system-config-samba | Samba GUI configuration tool (System \| Administration \| Server Settings \| Samba) |
| SWAT | Samba Web administration tool for configuring **smb.conf** with a Web browser; enables you to use a Web page interface to create and maintain your Samba configuration file, **smb.conf** |
| winbindd | Uses authentication services provided by Windows domain |

Name resolution and service announcements are handled by the `nmbd` server. Name resolution essentially resolves NetBIOS names with IP addresses. Service announcements, also known as *browsing*, are the way a list of services available on the network is made known to the connected Windows PCs (and Linux PCs connected through Samba).

Samba also includes the **winbindd** daemon, which allows Samba servers to use authentication services provided by a Windows domain. Instead of a Samba server maintaining its own set of users to allow access, it can make use of a Windows domain authentication service to authenticate users.

## Starting Up Samba

For a simple Samba setup, you should be able to use the default **/etc/samba/smb.conf** file installed with the Linux distribution package of Samba. If you need to make changes, however, you must restart the Samba server to have the changes take effect. Starting, stopping, and restarting the Samba server is managed by the **smb** and **nmb** scripts in the **/etc/rc.d/init.d/** directory, using the options **start**, **stop**, and **restart**. You can run the scripts using `nmb` and `smb` entries on the system-config-services Services panel (System | Administration | Server Settings | Services). You can also start them directly as shown here:

```
service smb restart
service nmb restart
```

To ensure name resolution, you can enter the name of your host and its IP address in the `/etc/samba/hosts` file. On Windows systems, `Lmhosts` entries consist of an IP address and the system's NetBIOS name, the name it is known by on a Microsoft network. For your Linux system, you can enter the IP address and the Linux system's hostname.

> **TIP** Be sure that you also start up the `nmb` server, not just the `smb` server. Without the `nmb` server, Windows cannot detect your Samba server.

## Firewalls

The `iptables` firewall prevents browsing Samba and Windows shares from your Linux desktop. To work around this restriction, you use `system-config-security` (System | Administration | Firewall and SELinux). Select the Samba entry in the Trusted services section. Firewall on your Windows computer and on your network router could, in turn, block Samba server access. Ensure your Windows and router firewalls are configured to accept the local IP address assigned by the router for computers on your network.

## Testing Samba from Linux

To test your connection from a Linux system, you can use the `smbclient` command to query the Samba server. To access the home directory of a user on the Samba server, use the IP or hostname address of the Samba server. With the `-U` option, specify a user to connect to on the system, as shown here:

```
smbclient -L //turtle.mytrek.com -U dylan
```

You are then prompted for a password. If the client password is different from the server password, use the server password. Once connected, you are presented with the SMB client prompt as shown here. You can then access the files on the user's home directory:

```
smb: \>
```

## Configuring Samba Access from Windows

To set up a connection for a Windows client, you need to specify the Windows workgroup name and configure the password. The workgroup name is the name that appears in the My Network Places on Windows 2000, NT, and XP (the Entire Network window in the Network Neighborhood on earlier Windows versions). To set the workgroup name on Windows XP, open System on the Control Panel, and on the Computer Name panel, click the Change button for the Rename Or Change Domain Entry. This opens a dialog window with a setting for the Workgroup, where you can enter the workgroup name. The default may be WORKGROUP or MSHOME. You can set up your own workgroup name, but all your computers would have to be configured to use that name.

On your Linux Samba server, in the **smb.conf** file, you specify the workgroup name in the **workgroup=** entry in the **global** section. The workgroup name should be uppercase and contain no spaces. The default name used on Windows XP systems is simply WORKGROUP. The **smb.conf** **workgroup** entry would then look like this:

```
workgroup = WORKGROUP
```

You can then restart the Samba server. On a Windows client, you see the Samba server listed when you select View Workgroups Computers from My Network Places. (On older Windows versions, use the Entire Network folder in your Network Neighborhood.) The Samba server will have as a name the description you gave it in your Samba configuration. Opening the icon will display a window with all the configured shares and printers on that Samba server.

To add a network place, in effect a shared Linux directory on the Samba server, click on the Add a Network Place entry in the Network Tasks panel for the My Network Places window. This starts the Add network place wizard, where, on the second dialog, you select Choose another network location. The following panel displays a Browse button and a text box for the network place. Click the Browse button, then in My Network Places, expand the Entire Network entry, and then Microsoft Windows Network. Here you should find listed your workgroup networks. Expand the workgroup you set up to use Samba. It should list both your Windows and Linux computers. Expand your Linux computer and select the shared directory you want to have listed in your My Network Places window.

## Samba Configuration File and Tools

Samba configuration options are kept in the /etc/samba/smb.conf file. You edit this file to make changes to the configuration. Once you finish making any changes, you should test your **smb.conf** file using the `testparm` program. The `testparm` program checks the validity of your configuration entries and lists your server definitions. By default, `testparm` uses the /etc/samba/smb.conf file, although you can supply a different configuration file as an argument:

```
testparm
```

To check your network connections, use the **smbstatus** command. This command returns a listing of all active SMB connections, showing the Windows computers you are connected to and your Linux shares.

> **NOTE** The /etc/samba/smbusers file associates Windows network usernames with corresponding users on your Linux Samba server. For example, *admin* and *administrator* are made equivalent to the Linux root user.

## User Level Security

Samba primarily provides user level security, requiring users on remote systems to log in using Samba registered passwords. Samba still provides share and server level access, but these methods have been deprecated and are not recommended. User level security requires the use of Windows encrypted passwords. Windows uses its own methods of encryption. For Samba to handle such passwords, it has to maintain its own Windows compatible password database. It cannot use the Linux password databases. Windows also uses additional information for the login process like where the user logged in.

User level security requires that each user that wants to login to a Samba share from a Windows system has to have a corresponding user account on the Samba server. In addition, for this account, you have to have a separate Samba password with which to login to the Samba share. In effect they become Samba users. The account on the Samba server does not have to have the same name as the one on the Windows system. A Windows user name can be specified for a Samba user. This mapping of Windows users to Samba (Linux) users is listed in the /etc/smbusers file. The following maps the Windows user rpetersen to the Samba (Linux) user richard.

```
richard = rpetersen
```

In the system-config-samba tool, you are allowed only to use users already created on your Samba server, but can specify a different Windows user. You also then enter the Samba password to use for that user. This is not the same as the password the user would ordinarily use for login on Linux.

When the Windows user in Windows tries to access the Samba share, the user will be prompted to log in. The Windows user would then enter rpetersen as the user name and the Samba password that was set up for richard.

User level security is managed by password backend databases. By default the tdbsam back end database is used. This is a tdb database file (trivial data base) that stores Samba passwords along with Windows extended information. The tdbsam database is designed for small networks. For systems using LDAP to manage users, you can use the LDAP enabled back end, ldbsam. The ldbsam database is designed for larger networks. The smbpasswd file previously used is still available, but is included only for backward compatibility. The default configuration entries for user access in the smb.conf file are shown here.

```
security = user
passdb backend = tdbsam
```

The username map option specifies the file used to associate Windows and Linux users. Windows users can use the Windows user name to log in as the associated user. The username map file is usually /etc/samba/smbusers. This is the file that both SWAT and system-config-samba use when setting up Samba users.

```
username map = /etc/samba/smbusers
```

If you are using an LDAP enabled Samba database, ldbsam, you would use special LDAP Samba tools to manage users. These are provided in the smblldap-tools package. They are prefixed with the term smblldap. There are tools for adding, modifying, and deleting users and groups like smblldap-useradd, smblldap-userdelete, and smblldap-groupmod. You use the smblldap-passwd command to manage Samba passwords with LDAP. The smblldap-userinfo to obtain information about a user. You configure your LDAP Samba tools support using the /etc/smblldap-tools/smblldap.conf file.

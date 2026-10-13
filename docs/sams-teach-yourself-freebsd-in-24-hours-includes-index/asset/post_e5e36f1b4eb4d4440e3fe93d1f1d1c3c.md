
```
# workgroup = NT-Domain-Name or Workgroup-Name, eg: REDHAT4
    workgroup = MYGROUP
```

Samba will now be started automatically when the system boots. To start it manually, run the samba.sh script with the start parameter:

```
# /usr/local/etc/rc.d/samba.sh start
Samba#
```

![](img/ba0161b65b37e94cffc801ecbacaba5e_417_0.png)

> Note that there is no line break in the script output after the service name Samba. This cosmetic flaw exists because during startup, each service in /usr/local/etc/rc.d is started sequentially, and the echoed output of each startup script all goes onto the same line. Being able to start services from the rc.d startup scripts is a convenience feature, not the primary intended functionality.

## The smbd and nmbd Daemons

If the samba.sh script runs successfully, you will notice two new processes running: smbd and nmbd

```
# ps -waux | grep mbd
root  3855  0.0  1.5  2368 1816  ??  Is   2:43PM  0:00.00
-/usr/local/sbin/smbd -D
root  3857  0.0  1.2  1040 1496  ??  Ss   2:43PM  0:00.02
-/usr/local/sbin/nmbd -D
```

The smbd daemon is the actual data server, the process that handles SMB/CIFS requests from connected Windows clients—file transfers, print jobs, listings, and so on. Unlike NFS, SMB doesn't require a separate process to be running for each simultaneous connection; the master smbd process forks off a new copy of itself for each new client session and handles all that client's requests for the duration of the session. The -D option specifies that smbd should operate as a standalone daemon, listening for requests on TCP port 139.

Operating in parallel with smbd is nmbd, the NetBIOS name server. It's the process that allows Windows clients to see the FreeBSD machine in the network browser view, as you saw in Figure 24.4. It also has the job of responding to client requests for a particular NetBIOS host if it's specified by name; if a Windows client uses the \\ <name> syntax to connect to a particular server by name, the client sends out a broadcast name request asking for the IP address of the server with that NetBIOS name. It's the job of nmbd to send back a response with the requested host's IP address so that the client can open an SMB request directly to the server. It's somewhat like DNS (in that it maps a common name to a direct address), and also has a lot in common with ARP (in that it operates on a LAN through broadcast name requests, rather than to a designated central name server).

## Creating Samba Shares

Many examples for how to configure a shared directory can be found in smb.conf.default. To enable any of them, remove the comment mark (#) from the beginning of the appropriate lines in smb.conf.

Example shares are displayed below the ===== Share Definitions ===== line in smb.conf. Each share's name is listed in brackets, and the configuration lines following it apply until the next bracketed block. The smb.conf file begins with a [global] block, allowing you to set global parameters that affect all shares on the system; the rest of the blocks each define a share whose settings override the previously defined global settings.

After making any configuration change in smb.conf, you will need to restart Samba by stopping and restarting it:

```
# /usr/local/etc/rc.d/samba.sh stop
# /usr/local/etc/rc.d/samba.sh start
```

![](img/ba0161b65b37e94cffc801ecbacaba5e_418_0.png)

> The man smb.conf page lists all available configuration parameters and describes in detail what each does. However, you might find it easier to view the page in HTML format—in which headings and examples are set apart with text formatting and made easier to read, as well as being contextually hyperlinked. Refer to the online documentation at http://samba.org/samba/docs/man/smb.conf.5.html for the formatted version.

## Sharing Directories

To share a regular public directory, define a share block like this:

```
[my-public]
comment = Public Stuff
path = /usr/local/share/samba-stuff
public = yes
writable = yes
printable = no
write list = @staff
```

With this share enabled, a client will see a share called my-public at the top level of the server's share listing. However, unless the user is authenticated and is a member of the UNIX group staff, the files in the share will be read-only. Remove the write list line to make the share writable by all users. Note that writable = yes is equivalent to saying read only = no.

By default, a [homes] share is defined and enabled; this special share is built-in, allowing access to each user's home directory on the Samba server if the Windows client connects to it with the proper credentials.

```
[homes]
comment = Home Directories
browseable = no
writable = yes
```

Because this share is set as not browsable, home directories not owned by the client user are not displayed; if a client connects as a valid user with a home directory on the Samba server, his home directory (labeled with his username because that's the name of the directory in UNIX) appears as one of the available shares. No other users' home directories appear.

## Sharing Printers

Like [homes], [printers] is a special share that behaves a little differently from regular shares. Under FreeBSD, all attached printers defined in /etc/printcap are available to Samba users. Chapter 9, “The FreeBSD Printing System,” explains how to set up your FreeBSD machine to support local printers in /etc/printcap.

By default, the [printers] share is set up like this:

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
# Set public = yes to allow user 'guest account' to print
guest ok = no
writable = no
printable = yes
```

Set browseable = yes to allow connected users to see and use your printers.

As stated in the embedded comment, you can make your printers public so that anyone on the network can use them. This involves the use of a guest user, which you can set up using share-level security. Note that public is a synonym for guest ok, so you would change the guest ok line to yes instead of adding a public = yes line to allow the guest user to print. Guest users and share-level security are a somewhat advanced topic; refer to the Samba Web site, or to the how-to guide at http://samba.linuxxbe.org/en/samba/config/share-1.html, for further documentation on how to use it.

## Access Control

The default method for controlling access to Samba shares is called *user-level security*. In this scheme, the client presents a username/password pair to the server upon the initial setup of the connection. The server determines whether to accept the client based on the username/password pair and the identity of the client machine itself. If it accepts the client, all shares are accessible.

It can be tricky to set up user-level security properly. The Windows username, which is defined either when the Windows user logs in to a local profile or to a domain controller, must exist on the Samba server as a regular UNIX user (or mapped to a UNIX user). For instance, if the Windows user Harris logs on to his Windows machine, opens up the Network Neighborhood window, and tries to connect to our Samba server, he will be denied access (and given a password prompt for a share called `\\STRIPES\\IPC$`) unless the user harris exists on the UNIX machine.

![](img/ba0161b65b37e94cffc801ecbacaba5e_420_0.png)

> In Windows NT/2000, the password prompt allows you to enter a username as well as a password. However, in Windows 95/98/ME, all you get is a password prompt, and the username is derived from the login name.

Samba users must exist in a password database at `/usr/local/private/smbpasswd`, which is similar to `/etc/master.passwd` in that encrypted passwords are stored in it for each local UNIX user. When Samba is installed, users from `/etc/master.passwd` are converted into Samba format and placed into `/usr/local/private/smbpasswd` with both the LANMAN password and the Windows NT password (both are present for compatibility) set to strings of 16 X characters—an invalid password, indicating that the user cannot log in.

To enable a user, you must set the password to something valid. This is done with the `smbpasswd` program. It works similarly to `passwd`, prompting you for your old Samba password and then requiring you to enter a new one twice unless you're root—in which case, you need not supply the old password, and you can change any user's password as well as your own.

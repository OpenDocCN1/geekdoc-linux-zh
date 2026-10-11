
Note that for this option to work there must be a working NIS system and the Samba server with this option must also be a logon server.

## nt acl support (S)
Default: *nt acl support = yes*

This boolean parameter controls whether smbd(8) will attempt to map UNIX permissions into Windows NT access control lists. This parameter was formally a global parameter in releases prior to 2.2.2.

## ntlm auth (G)
Default: *ntlm auth = yes*

This parameter determines whether or not smbd(8) will attempt to authenticate users using the NTLM encrypted password response. If disabled, either the lanman password hash or an NTLMv2 response will need to be sent by the client.

If this option, and **lanman auth** are both disabled, then only NTLMv2 logins will be permitted. Not all clients support NTLMv2, and most will require special configuration to use it.

## nt pipe support (G)
Default: *nt pipe support = yes*

This boolean parameter controls whether smbd(8) will allow Windows NT clients to connect to the NT SMB specific **IPC$** pipes. This is a developer debugging option and can be left alone.

## nt status support (G)
Default: *nt status support = yes*

This boolean parameter controls whether smbd(8) will negotiate NT specific status support with Windows NT/2k/XP clients. This is a developer debugging option and should be left alone. If this option is set to **no** then Samba offers exactly the same DOS error codes that versions prior to Samba 2.2.3 reported.

You should not need to ever disable this parameter.

## null passwords (G)
Default: *null passwords = no*

Allow or disallow client access to accounts that have null passwords.

See also smbpasswd(5).

## obey pam restrictions (G)
Default: *obey pam restrictions = no*

When Samba 3.0 is configured to enable PAM support (i.e. --with-pam), this parameter will control whether or not Samba should obey PAM's account and session management directives. The default behavior is to use PAM for clean text authentication only and to ignore any account or session management. Note that Samba always ignores PAM for authentication in the case of *encrypt passwords = yes*. The reason is that PAM modules cannot support the challenge/response authentication mechanism needed in the presence of SMB password encryption.

## only user (S)
Default: *only user = no*

This is a boolean option that controls whether connections with usernames not in the *user* list will be allowed. By default this option is disabled so that a client can supply a username to be used by the server. Enabling this parameter will force the server to only use the login names from the *user* list and is only really useful in *security = share level* security.

Note that this also means Samba won't try to deduce usernames from the service name. This can be annoying for the [*homes*] section. To get around this you could use *user = %S* which means your *user* list will be just the service name, which for home directories is the name of the user.

## oplock break wait time (G)
Default: *oplock break wait time = 0*

This is a tuning parameter added due to bugs in both Windows 9x and WinNT. If Samba responds to a client too quickly when that client issues an SMB that can cause an oplock break request, then the network client can fail and not respond to the break request. This tuning parameter (which is set in milliseconds) is the amount of time Samba will wait before sending an oplock break request to such (broken) clients.

> **WARNING**
>
> DO NOT CHANGE THIS PARAMETER UNLESS YOU HAVE READ AND UNDERSTOOD THE SAMBA OPLOCK CODE.

## oplock contention limit (S)
Default: *oplock contention limit = 2*

This is a *very* advanced smbd(8) tuning option to improve the efficiency of the granting of oplocks under multiple client contention for the same file.

In brief it specifies a number, which causes smbd(8) not to grant an oplock even when requested if the approximate number of clients contending for an oplock on the same file goes over this limit. This causes smbd to behave in a similar way to Windows NT.

**WARNING** DO NOT CHANGE THIS PARAMETER UNLESS YOU HAVE READ AND UNDERSTOOD THE SAMBA OPLOCK CODE.

## oplocks (S)
*Default: oplocks = yes*

This boolean option tells **smbd** whether to issue oplocks (opportunistic locks) to file open requests on this share. The oplock code can dramatically (approx. 30% or more) improve the speed of access to files on Samba servers. It allows the clients to aggressively cache files locally and you may want to disable this option for unreliable network environments (it is turned on by default in Windows NT Servers). For more information see the file **Speed.txt** in the Samba *docs/* directory.

Oplocks may be selectively turned off on certain files with a share. See the *veto oplock files* parameter. On some systems oplocks are recognized by the underlying operating system. This allows data synchronization between all access to oplocked files, whether it be via Samba or NFS or a local UNIX process. See the *kernel oplocks* parameter for details.

## os2 driver maps (G)
*Default: No default*

The parameter is used to define the absolute path to a file containing a mapping of Windows NT printer driver names to OS/2 printer driver names. The format is:

```
<nt driver name> = <os2 driver name>,<device name>
```

For example, a valid entry using the HP LaserJet 5 printer driver would appear as **HP LaserJet 5L = LASERJET.HP LaserJet 5L**.

The need for the file is due to the printer driver namespace problem described in Chapter 20, “Classical Printing Support”. For more details on OS/2 clients, please refer to Chapter 42, “Samba and Other CIFS Clients”.

## os level (G)
*Default: os level = 2065*

Example: *os level = 65*

This integer value controls what level Samba advertises itself as for browse elections. The value of this parameter determines whether **mbind(8)** has a chance of becoming a local master browser for the *workgroup* in the local broadcast area.

> *Note:* By default, Samba will win a local master browsing election over all Microsoft operating systems except a Windows NT 4.0/2000 Domain Controller. This means that a misconfigured Samba host can effectively isolate a subnet for browsing purposes. See **BROWSING.txt** in the Samba *docs/* directory for details.

## pam password change (G)
Default: *pam password change = no*

With the addition of better PAM support in Samba 2.2.2, this parameter, it is possible to use PAM's password change control flag for Samba. If enabled, then PAM will be used for password changes when requested by an SMB client instead of the program listed in *passwd program*. It should be possible to enable this without changing your *passwd chat* parameter for most setups.

## panic action (G)
Default: No default

Example: *panic action = \"/bin/sleep 90000\"*

This is a Samba developer option that allows a system command to be called when either smbd(8) or nmbd(8) crashes. This is usually used to draw attention to the fact that a problem occurred.

## paranoid server security (G)
Default: *paranoid server security = yes*

Some version of NT 4.x allow non-guest users with a bad password. When this option is enabled, samba will not use a broken NT 4.x server as password server, but instead complain to the logs and exit.

Disabling this option prevents Samba from making this check, which involves deliberately attempting a bad login to the remote server.

## passdb backend (G)
Default: *passdb backend = smbpasswd*

This option allows the administrator to choose which backends to retrieve and store passwords with. This allows (for example) both smbpasswd and tdbsam to be used without a recompile. Multiple backends can be specified, separated by spaces. The backends will be searched in the order they are specified. New users are always added to the first backend specified.

This parameter is in two parts, the backend's name, and a 'location' string that has meaning only to that particular backend. These are separated by a : character.

Available backends can include:

- **smbpasswd** - The default smbpasswd backend. Takes a path to the smbpasswd file as an optional argument.
- **tdbsam** - The TDB based password storage backend. Takes a path to the TDB as an optional argument (defaults to passdb.tdb in the *private dir* directory).
- **ldapsam** - The LDAP based passdb backend. Takes an LDAP URL as an optional argument (defaults to `ldap://localhost`).

LDAP connections should be secured where possible. This may be done using either Start-TLS (see *ldap ssl*) or by specifying `ldaps://` in the URL argument.

Multiple servers may also be specified in double-quotes, if your LDAP libraries supports the LDAP URL notation. (OpenLDAP does).

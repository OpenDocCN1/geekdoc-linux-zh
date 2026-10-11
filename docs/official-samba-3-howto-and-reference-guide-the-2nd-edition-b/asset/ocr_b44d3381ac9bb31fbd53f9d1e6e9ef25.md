# **ADS SEARCH** *EXPRESSION* *ATTRIBUTES*...

Perform a raw LDAP search on a ADS server and dump the results. The expression is a standard LDAP search expression, and the attributes are a list of LDAP fields to show in the results.

Example: `net ads search '(objectCategory=group)' sAMAccountName`

# **ADS DN** *DN (attributes)*

Perform a raw LDAP search on a ADS server and dump the results. The DN standard LDAP DN, and the attributes are a list of LDAP fields to show in the result.

Example: `net ads dn 'CN=administrator,CN=Users,DC=my,DC=domain' sAMAccountName`

# **WORKGROUP**

Print out workgroup name for specified kerberos realm.

# **HELP [COMMAND]**

Gives usage information for the specified command.

# **47.2 nmbd**

# Synopsis

```
```
nmbd [-D] [-F] [-S] [-a] [-i] [-o] [-h] [-V] [-d <debug level>] [-H
      <lmhosts file>] [-l <log directory>] [-p <port number>] [-s
      <configuration file>]
```
```

# **DESCRIPTION**

This program is part of the samba(7) suite.

**nmbd** is a server that understands and can reply to NetBIOS over IP name service requests, like those produced by SMB/CIFS clients such as Windows 95/98/ME, Windows NT, Windows 2000, Windows XP and LanManager clients. It also participates in the browsing protocols which make up the "Windows *Network Neighborhood*" view.

SMB/CIFS clients, when they start up, may wish to locate an SMB/CIFS server. That is, they wish to know what IP number a specified host is using.

Amongst other services, **nmbd** will listen for such requests, and if its own NetBIOS name is specified it will respond with the IP number of the host it is running on. Its "own NetBIOS name" is by default the primary DNS name of the host it is running on, but this can be overridden by the *netbios name* in **smb.conf**. Thus **nmbd** will reply to broadcast queries
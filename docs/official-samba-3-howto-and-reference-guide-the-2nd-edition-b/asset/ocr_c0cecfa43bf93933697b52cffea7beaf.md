# -n

This option specifies that the username following should have their password set to null (i.e. a blank password) in the local smbpasswd file. This is done by writing the string "NO PASSWORD" as the first part of the first password stored in the smbpasswd file.

Note that to allow users to logon to a Samba server once the password has been set to "NO PASSWORD" in the smbpasswd file the administrator must set the following parameter in the [global] section of the smb.conf file:

```
null passwords = yes
```

This option is only available when running smbpasswd as root.

# -r remote machine name

This option allows a user to specify what machine they wish to change their password on. Without this parameter smbpasswd defaults to the local host. The remote machine name is the NetBIOS name of the SMB/CIFS server to contact to attempt the password change. This name is resolved into an IP address using the standard name resolution mechanism in all programs of the Samba suite. See the -R name resolve order parameter for details on changing this resolving mechanism.

The username whose password is changed is that of the current UNIX logged on user. See the -U username parameter for details on changing the password for a different username.

Note that if changing a Windows NT Domain password the remote machine specified must be the Primary Domain Controller for the domain (Backup Domain Controllers only have a read-only copy of the user account database and will not allow the password change).

Note that Windows 95/98 do not have a real password database so it is not possible to change passwords specifying a Win95/98 machine as remote machine target.

# -R name resolve order

This option allows the user of smbpasswd to determine what name resolution services to use when looking up the NetBIOS name of the host being connected to.

The options are "lmhosts", "host", "wins" and "bcast". They cause names to be resolved as follows:

+   * lmhosts: Lookup an IP address in the Samba lmhosts file. If the line in lmhosts has no name type attached to the NetBIOS name (see the lmhosts(5) for details) then any name type matches for lookup.

+   * host: Do a standard host name to IP address resolution, using the system /etc/hosts, NIS, or DNS lookups. This method of name resolution is operating system depended for instance on IRIX or Solaris this may be controlled by the /etc/nsswitch.conf file. Note that this method is only used if the NetBIOS name type being queried is the 0x20 (server) name type, otherwise it is ignored.

+   * wins: Query a name with the IP address listed in the wins server parameter. If no WINS server has been specified this method will be ignored.
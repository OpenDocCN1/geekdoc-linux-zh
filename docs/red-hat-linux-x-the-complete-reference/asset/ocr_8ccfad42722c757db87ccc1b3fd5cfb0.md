# Domain Logons

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

# Domain Master specifies Samba to be the Domain Master Browser. This
# allows Samba to collate browse lists between subnets. Don't use this
# if you already have a Windows NT domain controller doing this job
`;   domain master = yes`

# Preferred Master causes Samba to force a local browser election on startup
# and gives it a slightly higher chance of winning the election
`;   preferred master = yes`

# Enable this if you want Samba to be a domain logon server for
# Windows95 workstations.
`;   domain logons = yes`

# if you enable domain logons then you may want a per-machine or
# per user logon script
# run a specific logon batch file per workstation (machine)
`;   logon script = %m.bat`
# run a specific logon batch file per username
`;   logon script = %U.bat`

# All NetBIOS names must be resolved to IP Addresses
# 'Name Resolve Order' allows the named resolution mechanism to be specified
# the default order is "host lmhosts wins bcast". "host" means use the unix
# system gethostbyname() function call that will use either `/etc/hosts` OR
# DNS or NIS depending on the settings of `/etc/host.config`, `/etc/nsswitch.conf`
# and the `/etc/resolv.conf` file. "host" therefore is system configuration
# dependent. This parameter is most often used to prevent DNS lookups
# in order to resolve NetBIOS names to IP Addresses. Use with care!
# The example below excludes use of name resolution for machines that are NOT
# on the local network segment
# - OR - are not deliberately to be known via lmhosts or via WINS.
`; name resolve order = wins lmhosts bcast`

# Windows Internet Name Serving Support Section:
# WINS Support - Tells the NMBD component of Samba to enable its WINS Server
```
; wins support = yes
```

# WINS Server - Tells the NMBD components of Samba to be a WINS Client
#       Note: Samba can be either a WINS Server, or a WINS Client, but NOT both
`; wins server = w.x.y.z`

# WINS Proxy - Tells Samba to answer name resolution queries on
# behalf of a non WINS capable client, for this to work there must be
# at least one      WINS Server on the network. The default is NO.
`; wins proxy = yes`

# DNS Proxy - tells Samba whether or not to try to resolve NetBIOS names
# via DNS nslookups. The built-in default for versions 1.9.17 is yes,
# this has been changed in version 1.9.18 to no.
`dns proxy = no`

# Case Preservation can be handy - system default is _no_
# NOTE: These can be set on a per share basis
`; preserve case = no`
`; short preserve case = no`
# Default case is normally upper case for all DOS files
`; default case = lower`
# Be very careful with case sensitivity - it can break things!
`; case sensitive = no`

## Share Definitions
```
[homes]
    comment = Home Directories
    browseable = no
    writable = yes
```

# Un-comment the following and create the netlogon directory for Domain Logons
```
; [netlogon]
;   comment = Network Logon Service
```

## 清单 16-1 续
```
; path = /home/netlogon
; guest ok = yes
; writable = no
; share modes = no
```

# Un-comment the following to provide a specific profile share
# the default is to use the user's home directory
```
;[Profiles]
; path = /home/profiles
; browseable = no
; guest ok = yes
```

# NOTE: If you have a BSD-style print system there is no need to
# specifically define each individual printer
```
[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = no
# Set public = yes to allow user 'guest account' to print
    guest ok = no
    printable = yes
```

# This one is useful for people to share files
```
;[tmp]
; comment = Temporary file space
; path = /tmp
; read only = no
; public = yes
```

# A publicly accessible directory, but read only, except for people in
# the "staff" group
```
;[public]
; comment = Public Stuff
; path = /home/samba
```

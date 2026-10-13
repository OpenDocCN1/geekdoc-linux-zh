# Listing 11-1 Continued

```
# Preferred Master causes Samba to force a local
# browser election on startup and gives it a slightly
# higher chance of winning the election
;    preferred master = yes

# Use only if you have an NT server on your
# network that has been configured at install time
# to be a primary domain controller.
;    domain controller = <NT-Domain-Controller-SMBName>

# Enable this if you want Samba to be a domain
# logon server for Windows95 workstations.
;    domain logons = yes

# If you enable domain logons then you may want
# a per-machine or per user logon script run a
# specific logon batch file per workstation (machine)
;    logon script = %m.bat
# run a specific logon batch file per username
;    logon script = %U.bat

# Where to store roving profiles (only for Win95
# and WinNT) %L substitutes for this servers
# netbios name, %U is username
# You must uncomment the [Profiles] share below
;    logon path = \\%L\Profiles\%U

# All NetBIOS names must be resolved to
# IP Addresses 'Name Resolve Order' allows
# the named resolution mechanism to be specified
# the default order is "host lmhosts wins bcast".
# "host" means use the unix system gethostname()
# function call that will use either /etc/hosts OR
# DNS or NIS depending on the settings of
```
```
```
AuthorizationFile           authorization
HostKeyFile                 hostkey
PublicHostKeyFile           hostkey.pub
RandomSeedFile              random_seed
ForwardAgent                        yes
ForwardX11                          yes

# DEPRECATED              PasswordAuthentication        yes
    PasswordGuesses               3
#   MaxConnections              50
# 0 == number of connections not limited
    MaxConnections                0
#   PermitRootLogin             nopwd
    PermitRootLogin               yes
# DEPRECATED                PubkeyAuthentication          yes
#
#   AllowedAuthentications      publickey,password,hostbased
    AllowedAuthentications        publickey,password
#   RequiredAuthentications     publickey,password
    ForcePTYAllocation                no
    VerboseMode                         no
    PrintMotd                         yes
    CheckMail                         yes
    UserConfigDirectory     "%D/.ssh"
#   UserConfigDirectory     "/etc/ssh2/auth/%U"
    SyslogFacility            AUTH
#   SyslogFacility            LOCAL7
    Ssh1Compatibility             yes
#
#   SshldPath         <set by   configure>
#
#   AllowHosts          localhost, foobar.com, friendly.org
#   DenyHosts           evil.org, aol.com
#   AllowHosts          trusted.host.org
#   DenyHosts           not.quite.trusted.org
#
#   IgnoreRhosts                  no
#   IgnoreRootRhosts              no
# (the above, if not set, is defaulted to the value of IgnoreRhosts)
#
    NoDelay                           yes
#
    KeepAlive                       yes
    RequireReverseMapping           no
```
```
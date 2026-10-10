```
#     AllowedAuthentications       publickey,password
#     RequiredAuthentications      publickey,password
#     HostbasedAuthForceClientHostnameDNSMatch no
#     SshPAMClientPath            ssh-pam-client
```

Table 2.12 describes the authentication options available for the SSH server.

**Table 2.12  Options in the Authentication Section (Unix)**
| OPTION | DESCRIPTION |
| --- | --- |
| BannerMessageFile | Identifies the location of the file that contains the text to be displayed before the client logs in to the SSH server. This is very useful for legal disclaimers. |
| PasswordGuesses | Identifies the number of attempts a user is given before being disconnected if valid authentication is not submitted. |
| AllowedAuthentications | Identifies the types of authentication methods that are valid. Options include password, publickey, and hostbased. |
| RequiredAuthentications | Identifies the types of authentication methods required for authentication. If the value is empty, any values in AllowedAuthentication will be honored. |
| HostbasedAuthForceClientHostnameDNSMatch | Requires an exact match of the SSH client's hostname and the client's DNS entry. |
| SshPAMClientPath | Identifies the location of the SSH PAM client to use in order for PAM authentication to take place. The default location is */usr/local/bin/ssh-pam-client*. |

# *Host Restrictions*

The Host Restrictions section of the sshd2_config file should look like the following:

```
#AllowHosts                localhost, foobar.com, friendly.org
##AllowHosts                t,.,l,.,*
##    AllowHosts            [{{digit}:1}{,3}\{,3}{{digit}:1}{,3}
##    AllowHosts            \i,.*
##
#    DenyHosts             evil.org, ool.com
#    AllowHosts            trusted\.host\.org
#    DenyHosts             not\.quite\.trusted\.org
#    IgnoreRootRhosts      no
#                           no
```
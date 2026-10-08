# rpcgen

# Examples

The following example shows the output of the roles command for three users.

```
mopoke% roles winsor ray des
winsor : printadm
ray : printadm
roles: des : No roles
mopoke%
```

The output shows that users winsor and ray are both members of the printadm role. User des is not assigned to any roles.

# Exit Status

+   0 Successful completion.
1 An error occurred.

# Files

+   /etc/security/exec_attr
Execution profiles database.
/etc/security/prof_attr
Profile description database.
/etc/user_attr
Extended user attributes database.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwcs |

# See Also

auths(1), pfexec(1), profiles(1), login(1), su(1M), getauusername(3BSM), auth_attr(4), passwd(4), shadow(4), user_attr(4), attributes(5)

# rpcgen — RPC Protocol Compiler

# Synopsis

```
/usr/bin/rpcgen [-a] [-A] [-b] [-C] -Dname = value] [-i size]
-I [-K seconds] [-L] [-M] [-N] [-T] [-v] [-Y Pathname] infile
/usr/bin/rpcgen [-c -h -l -m -t -Sc -Ss -Sm -o outfile]
infile - *
```
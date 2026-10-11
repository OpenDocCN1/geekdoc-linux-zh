Please note that setting this parameter to + causes problems with group membership at least on glibc systems, as the character + is used as a special character for NIS in /etc/group.

# **winbind trusted domains only (G)**  Default: *winbind trusted domains only* = *no*

This parameter is designed to allow Samba servers that are members of a Samba controlled domain to use UNIX accounts distributed via NIS, rsysnc, or LDAP as the uid's for winbindd users in the hosts primary domain. Therefore, the user DOMAIN\user1 would be mapped to the account user1 in /etc/passwd instead of allocating a new uid for him or her.

# **winbind use default domain (G)**  Default: *winbind use default domain* = *noyes*

Example: *winbind use default domain* = *yes*

This parameter specifies whether the winbindd(8) daemon should operate on users without domain component in their username. Users without a domain component are treated as is part of the winbind server's own domain. While this does not benefit Windows users, it makes SSH, FTP and e-mail function in a way much closer to the way they would in a native unix system.

# **wins hook (G)**  Default: *No default*

When Samba is running as a WINS server this allows you to call an external program for all changes to the WINS database. The primary use for this option is to allow the dynamic update of external name resolution databases such as dynamic DNS.

The wins hook parameter specifies the name of a script or executable that will be called as follows:

```
wins hook operation name nametype ttl IP_list
```

+   - The first argument is the operation and is one of "add", "delete", or "refresh". In most cases the operation can be ignored as the rest of the parameters provide sufficient information. Note that "refresh" may sometimes be called when the name has not previously been added, in that case it should be treated as an add.
+   - The second argument is the NetBIOS name. If the name is not a legal name then the wins hook is not called. Legal names contain only letters, digits, hyphens, underscores and periods.
+   - The third argument is the NetBIOS name type as a 2 digit hexadecimal number.
+   - The fourth argument is the TTL (time to live) for the name in seconds.
+   - The fifth and subsequent arguments are the IP addresses currently registered for that name. If this list is empty then the name should be deleted.

An example script that calls the BIND dynamic DNS update program *nsupdate* is provided in the examples directory of the Samba source code.
# Configure slapd for Replication

The slapd on the master server can be configured to write a replication logfile by the following entry /etc/openldap/slapd.conf:

```
replogfile /var/lib/ldap/master-slapd.replog
```

This file contains regular LDIF change records, e.g.

```
time: 1148659780
dn: ou=groups,dc=digitalairlines,dc=com
changetype: add
objectClass: organizationalUnit
ou: groups
structuralObjectClass: organizationalUnit
entryUUID: c7b0c4e0-811d-102a-9c4d-2129ebe1b381
creatorsName: cn=Administrator,dc=digitalairlines,dc=com
createTimestamp: 20060526160940Z
entryCSN: 20060526160940Z#000000#00000000
modifiersName: cn=Administrator,dc=digitalairlines,dc=com
modifyTimestamp: 20060526160940Z
```

On the master server you have to specify the name(s) of the slave server(s) with the replica option:

```
replica uri=ldap://10.0.0.51:389
binddn="cn=replicator,dc=digitalairlines,dc=com" bindmethod=simple
credentials=novell
```

The following parameters are used:

+   - **uri**. Name or IP of the slave server. The default LDAP port is 389. If you want to use LDAPS (port 636), the uri looks like this
+   **replica uri=ldaps://10.0.0.51:636 ...**

+   - **binddn**. DN of the master server that is allowed to access the slave. This DN must also be specified on the slave server with the option updatedn.
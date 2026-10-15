
## Objective 3 Replicate OpenLDAP Servers

If there are a lot of requests for the LDAP server you may need more than one server. One server is the master. The other servers are slaves. A master/slave arrangement provides an effective way to increase capacity, availability, and reliability.

Changes on the master server are propagated by the slurpd to the slaves. In this objective we cover the following topics:

- Add the Replication DN to the LDAP Directory
- Configure slapd for Replication
- The Command-Line Options of slurpd
- Transfer the LDAP Database

## Add the Replication DN to the LDAP Directory

In the LDAP directory (on master and slave) there must be an object with the DN used for replication. This can look like this:

```
dn: uid=replicator,dc=digitalairlines,dc=com
objectClass: inetOrgPerson
uid: Replicator
cn: LDAP Replicator
sn: Replicator
```

You also have to set a password for this object using ldappasswd.

## Configure slapd for Replication

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

- **uri**. Name or IP of the slave server. The default LDAP port is 389. If you want to use LDAPS (port 636), the uri looks like this
**replica uri=ldaps://10.0.0.51:636 ...**

- **binddn**. DN of the master server that is allowed to access the slave. This DN must also be specified on the slave server with the option updatedn.

This DN should not be the same as the master’s rootdn.

- **bindmethod.** Specifies the authentication method. You can select between **simple** (password-based authentication) and **sasl** (SASL authentication).
- **credentials.** Password for simple authentication.

On the slave server you have to add the **updatedn** option, as mentioned. For example:

```
updatedn="cn=replicator,dc=digitalairlines,dc=com"
```

Use the **updateref** directive to define the URL the slave should return if an update request is received.

```
updateref="ldap://10.0.0.51"
```

You have to make sure that this DN has permission to write the database (e.g., by **access** directives).

```
access to *
  by dn="cn=replicator,dc=digitalairlines,dc=com" write
  by * read
```

## The Command-Line Options of slurpd

The man page of slurpd can be accessed by man 8 slurpd.

The options of slurpd are:

- **-d level**. Specify the debug level. Possible debug levels are:
  - 4. Heavy trace debugging
  - 64. Configuration file processing
  - 65535. Enable all debugging
  - ?. Lists all debug levels and exits slurpd.
- **-f file**. Specifies the slapd configuration file. The default is /etc/openldap/slapd.conf.
- **-r file**. Specifies the name of the slapd replication logfile.
- **-o**. Run in "one-shot" mode. Normally, slurpd processes the replog file and then watches for more replication entries to be appended. In one-shot mode, slurpd processes a replication log and exits.
- **-t directory**. slurpd copies the replication log to a working directory before processing it.

There is a start script available in /etc/init.d/ and you can start the slurpd by entering rcslurpd start.

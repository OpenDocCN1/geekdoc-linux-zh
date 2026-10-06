# Server-Side Daemons

The server side consists of two main daemons:

+   - slapd This is a stand-alone LDAP daemon that listens for LDAP connections from clients and responds to the LDAP operations it receives over those connections.

+   - slurpd This a stand-alone LDAP replication daemon that is used to propagate changes from one slapd to another. This daemon is used for synchronizing changes from one LDAP server to another. It is needed when more than one LDAP server is in use.

# OpenLDAP Utilities

The OpenLDAP utilities are a set of command-line tools for querying, viewing, updating, and modifying the data stored in the OpenLDAP directory. On Fedora, Red Enterprise Linux (RHEL), and CentOS they are provided by the openldap-clients*.rpm package, and some of them are provided by the openldap-servers*.rpm package. The programs are listed and described in Table 27-1.

| Utility | Description |
| --- | --- |
| ldapmodify | Used for modifying entries in LDAP. It accepts either input directly from the command line or via a file. |
| ldapadd | A hard link to ldapmodify -a command. It is used to add new entries to an LDAP database. (The functionality provided by the ldapadd command can be obtained by adding more than one option to the ldapmodify command.) |
| ldapdelete | Used for deleting entries from an OpenLDAP directory. |
| ldpasswd | Sets the password for an LDAP user. |
| ldapsearch | Used for querying/searching an LDAP directory. |
| slapadd | Accepts input from an LDIF file to populate an LDAP directory. Located under the `/usr/sbin/`. |
| slapcat | Dumps the contents of the LDAP directory into an LDAP-type file. Located under the `/usr/sbin/`. |
| slapindex | Used for reindexing the LDAP database according to the actual current database content. Located under the `/usr/sbin/`. |
| slappasswd | Used for generating properly hashed/encrypted passwords that can be used with various privileged directory operations. Located under the `/usr/sbin/`. |

Table 27-1 OpenLDAP Utilities
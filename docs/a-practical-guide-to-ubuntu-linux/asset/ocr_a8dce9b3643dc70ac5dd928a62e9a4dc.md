# LDAP

LDAP (Lightweight Directory Access Protocol) is an alternative to the older X.500 DAP (Directory Access Protocol). It runs over TCP/IP and is network aware, standards based, and available on many platforms. It queries an LDAP server, specifying the data it wants. For example, a query could ask for the first names and email addresses of all people with a last name of Smith who lives in San Francisco.

Directory is designed to work with data that does not change frequently, the server holds a search and read optimized database, called a directory. LDAP clients query and update this directory.

In addition to name and address information, an LDAP directory can hold lists of network services. Or, other services can use it for authentication. LDAP is appropriate for any kind of relatively structured information where fast lookups are required. Many types of clients are set to communicate with LDAP servers, including LDAP-specific clients (page 767), email clients, and authentication services.

Ubuntu provides the OpenLDAP (www.openldap.org) implementation of LDAP. OpenLDAP uses the Berkeley DB (Berkeley DB, now BDB by Oracle), which meets the needs of an LDAP database. It supports distributed architecture, replication, and encryption. LDAP differs from a relational database (RDBMS): Instead of holding information in rows and columns, DB implements an LDAP directory as a hierarchical data structure that groups information with similar attributes. This section describes OpenLDAP.

In addition to BDB, Ubuntu supplies HDB, which is based on BDB but provides faster writers than BDB does. It also supports subtree renaming, which allows subtrees to be moved efficiently within a database. Ubuntu HDB is the default LDAP database.

An entry (a node in the LDAP directory hierarchy, or a container) is the basic unit of information in an LDAP directory. Each entry has one or more attributes. Each attribute has a name (attribute type or description) and one or more values. Attribute names come from a standard schema that is held in files found in the /etc/ldap schema directory. This schema is standard across many implementations of LDAP, allowing LDAP clients to obtain data from many LDAP servers. Although it is not necessarily necessary or advisable, you can change or modify the schema.

A Distinguished (DN) uniquely identifies each entry in an LDAP directory. A DN comprises a Relative Distinguished Name (RDN), which is constructed from one or more attributes in the entry, followed by the DN of the parent entry. Because it can change (e.g, a woman may change her last), and because of content, unique identifier is sometimes required, the server assigns a UUID (unambiguous identifier) to each entry.

The DSE (DSA-Specific Entry) is the root, or top-level, entry in an LDAP directory. (DSA stands for Directory System Agent). The DSE specifies the domain name of the server and is defined in the /etc/ldap/slapd.d hierarchy. LDAP defines a domain
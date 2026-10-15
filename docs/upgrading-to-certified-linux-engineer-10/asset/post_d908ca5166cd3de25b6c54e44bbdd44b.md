
## Example 2:

```
access to *
by dn="cn=Administrator,dc=digitalairlines,dc=com" write
by * read
```

- **database**. Specifies the kind of back end. The following databases are supported:
- bdb. Berkeley DB
- dnssrv. DNS SRV
- hdb. A hierarchical variant of bdb
- ldap. Lightweight Directory Access Protocol (Proxy)
- ldbm. Lightweight DBM
- meta. Meta directory
- monitor. Monitor backend
- passwd. Read-only access to passwd
- perl. Perl programmable backend
- shell. External shell program
- sql. SQL programmable backend

- **suffix "DN"**
Specify the DN suffix of queries that will be passed to this backend database.
Example:

```
suffix    "dc=digitalairlines,dc=com"
```

- **checkpoint ops minutes**. Checkpoints are only tested after successful write operations. If ops operations have been completed or more than the specified number of minutes have passed, a new checkpoint is performed.

Possible **types** are:

- **pres.** Allows filters to be used that ask if the attribute is present in an entry (cn=*).
- **eq.** Allows filters to be used that ask if an attribute has an exact value. It includes presence, so it is not necessary to index something as pres,eq.
- **approx.** Allows filters to be used that ask if an attribute value is “similar to” something.
- **sub.** Allows filters to be used that do substring searches on an attribute's values.
- **none.**

After finishing the configuration, you can start the server with the following command:

```
rcldap start
```

If you want to start the LDAP server automatically when the server boots, use the following command:

```
insserv ldap
```

## Configure the LDAP Clients with ldap.conf

After you have changed the server configuration file, you need to change the client configuration. Two files are important:

- /etc/openldap/ldap.conf
- /etc/ldap.conf

## /etc/openldap/ldap.conf

The file /etc/openldap/ldap.conf is the configuration file of the LDAP client.

The most important options are specified below:

- **host 127.0.0.1**
  This line sets the default server that LDAP clients should connect to.

- **base dc=digitalairlines,dc=com**
  This is the default directory search base that should be used by LDAP clients.

After a standard installation, there is one more line in /etc/ldap.conf:

```
TLS_REQCERT    allow    ............
```

TLS_REQCERT specifies what checks, if any, to perform on server certificates in a TLS session. The level can be specified as one of the following keywords:

- **never**. The client will not request or check any server certificate.
- **allow**. The server certificate is requested. If no certificate or a bad certificate is provided, the session proceeds normally.
- **try**. The server certificate is requested. If no certificate is provided, the session proceeds normally. If a bad certificate is provided, the session is immediately terminated.
- **demand or hard**. The server certificate is requested. If no certificate or a bad certificate is provided, the session is immediately terminated. (default)

For more options, read the manual man 5 ldap.conf.

## /etc/ldap.conf

The file /etc/ldap.conf is the configuration file for the LDAP nameservice switch library, the LDAP PAM module, and the shadow package. The file belongs to the RPM package pwdutils.

```
da51:~ # rpm -qf /etc/ldap.conf
pwdutils-3.0.7.1-17.10
da51:~ #
```

The most important options of /etc/ldap.conf are:

- **host.** Specifies the name(s) or IP address(es) of the LDAP server(s) to connect to.
- **base.** Specifies the default base distinguished name (DN) to use for searches.
- **ldap_version.** Specifies the version of the LDAP protocol; “3” stands for LDAPv3.
- **bind_policy.** Specifies what happens if the LDAP server is not reachable. The possible values are:
  - **hard.** nss_ldap will retry connecting to the software with exponential backoff. (default)
  - **soft.** Forbids nss_ldap from retrying failed LDAP queries.
- **binddn.** Specifies the distinguished name with which to bind to the directory server(s). The default is to bind anonymously.
- **bindpw.** Specifies the cleartext credentials with which to bind. This option is only applicable when used with binddn above.
- **scope.** Specifies the search scope. Possible values are:
  - **sub.** subtree
  - **one.** one level
  - **base.** base object

# Example 2:

```
access to *
by dn="cn=Administrator,dc=digitalairlines,dc=com" write
by * read
```

+   - **database**. Specifies the kind of back end. The following databases are supported:

+   - bdb. Berkeley DB
+   - dnssrv. DNS SRV
+   - hdb. A hierarchical variant of bdb
+   - ldap. Lightweight Directory Access Protocol (Proxy)
+   - ldbm. Lightweight DBM
+   - meta. Meta directory
+   - monitor. Monitor backend
+   - passwd. Read-only access to passwd
+   - perl. Perl programmable backend
+   - shell. External shell program
+   - sql. SQL programmable backend

+   - **suffix "DN"**
+   Specify the DN suffix of queries that will be passed to this backend database.
+   Example:

```
suffix    "dc=digitalairlines,dc=com"
```

+   - **checkpoint ops minutes**. Checkpoints are only tested after successful write operations. If ops operations have been completed or more than the specified number of minutes have passed, a new checkpoint is performed.
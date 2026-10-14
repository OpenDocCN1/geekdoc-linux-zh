authentication, such as LDAP (see -l option next). Just insert a new entry in the database, and the account is ready to go. No need to create any directory for that user: It will be automatically created the first time he or she logs in.

+   - `-l authentication_method: filename` enables a new authentication method and specifies the file containing authentication data. The method can be one of the following:
+     - `unix` for standard (`/etc/passwd`) authentication
+     - `pam` for PAM authentication
+     - `ldap:LDAP_config_file` for LDAP directories
+     - `mysql:MySQL_config_file` for MySQL databases
+     - `pgsql:Postgres_config_file` for Postgres databases
+     - `puredb:PureDB_database_file` for PureDB virtual user databases
+     - `extauth:path` to pure-authd socket for external authentication handlers

PAM is assumed by default if the server was compiled with PAM support, and Unix is assumed by default otherwise. The SUSE version has PAM support included.

Multiple authentication methods can be specified concurrently. For instance, you can run the server with `-puredb:/etc/pwd.pdb -mysql:/etc/my.cf -lunix`. The users will first be authenticated from a PureDB database. If this method fails, a MySQL server will be queried. If the account is still not found, standard Linux accounts will be scanned. Authentication methods are tried in the order you give the `-l` options. Refer to the README.LDAP and README.MySQL files in `/usr/share/doc/packages/pure-ftpd` for information about built-in LDAP and SQL directory support, or visit `http://www.pureftpd.org/documentation.shtml`.

+   - `-R` disallows the use of the chmod command. This is a nice security feature because users are not able to change the file permissions on files uploaded by others or those that are available for download.
+   - `-S host,port` specifies the IP address and port that will accept incoming connections. This option is useful if the server has multiple NICs and you wish to limit FTP traffic to just one. This option can be used only in standalone mode.
+   - `-u #` doesn't allow UIDs below `#`. If you specify `-u 1`, the root user will be denied access, which may be a good idea.
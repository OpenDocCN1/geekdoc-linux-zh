+   3. Verify that the server is running.
+   4. Edit the configuration files.

# INSTALL THE GRANTS TABLE

Before MySQL can be used you need to install the grants table. The grants table is a database which contains user information and permissions. You can install the initial grants table using the mysql_install_db script, which is located in the /usr/local/bin/ directory:

```
# /usr/local/bin/mysql_install_db
Creating db table
Creating host table
Creating user table
Creating func table
Creating tables_priv table
Creating columns_priv table
```

To start mysqld at boot time you have to copy support-files/mysql.server
to the right place for your system

```
PLEASE REMEMBER TO SET A PASSWORD FOR THE MySQL root USER !
This is done with:
/usr/local/mysql/bin/mysqladmin -u root password 'new-password'
See the manual for more instructions.
```

Please report any problems with the /usr/local/mysql/bin/mysqlbug script!

The latest information about MySQL is available on the web at http://www.mysql.com
Support MySQL by buying support/licenses at http://www.tcx.se/license.html.

The initial grants table contains the following settings:

+   - A MySQL root user is created with super-user privileges. The root user can only be used for connections from the local server host.
+   - An anonymous user is created which can perform any operation on databases named test or databases with names starting with test_. The anonymous user can only be used for connections from the local server host.
+   - Other privileges are denied.

# START mysqld

To start the mysqld daemon, do not directly invoke the /usr/local/libexec/mysqld program but instead use the /usr/local/bin/safe_mysqld script, which sets up the necessary environment and then starts mysqld:

```
# cd /usr/local
# bin/safe_mysqld &
Starting mysqld daemon with databases from /usr/local/var
```
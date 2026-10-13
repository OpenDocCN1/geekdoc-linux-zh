```
sort_buffer              | 2097144
table_cache              | 64
thread_stack             | 65536
tmp_table_size           | 1048576
tmpdir                   | /tmp/
version                  | 3.22.30
wait_timeout             | 28800
```

Finally, you can conduct further tests using the mysqlshow command to show existing databases, tables, and records. For instance, to display a list of existing tables, use the command without any parameters:

```
# /usr/local/bin/mysqlshow
+-----------+
| Databases |
+-----------+
| mysql     |
| test      |
+-----------+
```

# SET THE root PASSWORD

When the initial grants table is installed, the root user has no password. This is a gaping security hole because it enables any user with shell access to use the MySQL server as the root database user. After you have verified correct operation of the server, your first order of business should be to set a root password.

To do this, use the mysqladmin command:

```
# /usr/local/bin/mysqladmin -u root password <new password>
```

After you have set a password, it is necessary to specify the username and password for most actions. For instance, the mysqladmin version command used above now needs to be issued as follows:

```
# /usr/local/bin/mysqladmin -u root --password=<password> version
```

# EDIT THE CONFIGURATION FILES

You can specify default start-up options for all MySQL applications such as mysqladmin, mysql, or mysqld using options files. You can create three possible options files:

+   - `/etc/my.cnf`
+   - `/usr/local/var/my.cnf`
+   - `~/.my.cnf`

MySQL applications will read the files in this order and settings from later options file will always take precedence over earlier files.

An options file consists of a series of sections of the general form:
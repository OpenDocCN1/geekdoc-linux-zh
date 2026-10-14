+   - /etc/postgresql/8.4/main/postgresql.conf

The /etc/postgresql/8.4/main/ directory contains the main configuration files for PostgreSQL 8.4, with postgresql.conf being the primary configuration file. This file is heavily commented, so you can use the file as a reference when you change options.

+   - /etc/postgresql/8.4/main/pg_hba.conf

This is the configuration file that stores all host authentication information. Here you can control which hosts on the network can access the PostgreSQL database.

+   - /etc/postgresql/8.4/main/pg_ident.conf

The pg_ident.conf file allows you to map a local username on the server to a different PostgreSQL username. So if your local username and PostgreSQL username don't match, you can add a mapping here and avoid having to add the PostgreSQL username to the command line each time you run psql.

+   - /etc/init.d/postgresql-8.4

This is the init script for PostgreSQL 8.4. As you can see, Ubuntu labels the init script based on the database version, so you can install and use multiple PostgreSQL versions on the same host.

+   - /var/log/postgresql/

Unlike MySQL, which logs to syslog, PostgreSQL separates all of its logging under /var/log/postgresql. From there each log is labeled according to its version, so the default PostgreSQL 8.4 database under Lucid logs to /var/log/postgresql/postgresql-8.4-main.log.

# Web-Based PostgreSQL Administration

If you think hard-core MySQL administrators balk at Web-based administration, you should see how hard-core PostgreSQL administrators react. Even so, if you just want to create a Web site that is backed on a solid PostgreSQL database, you might appreciate the simplicity of managing the database from the Web. As with MySQL, there is a PHP-based administration tool called phpPgAdmin. To install phpPgAdmin, you simply need to install the phppgadmin package:

```
$ sudo apt-get install phppgadmin
```
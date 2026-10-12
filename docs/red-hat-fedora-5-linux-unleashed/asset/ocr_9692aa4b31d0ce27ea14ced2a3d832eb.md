# TABLE 22.2 Continued

| Option | Action |
| --- | --- |
| -U username | Connects to the database as the user username. |
| -W | Prompts for a password after connecting to the database. In PostgreSQL 7 and later, password prompting is automatic if the server requests a password after a connection has been established. |
| -? | Displays a help message. |

Several more options are available in addition to those listed in Table 22.2. See the `psql`'s man page for details on all the available options.

# Graphical Clients

If you'd rather interact with a database by using a graphical database client than with the command-line clients discussed in the previous section, you're in luck: A few options are available.

MySQL has an official graphical client, called MySQL GUI. MySQLGUI is available in both source and binary formats from the MySQL website at http://www.mysql.com/.

Web-based administration interfaces are also available for MySQL, and PostgreSQL. phpMyAdmin and phpPgAdmin are two such products. Both of these products are based on the PHP-embedded scripting language and therefore require you to have PHP installed. Of course, you also need to have a web server installed.

# RELATED FEDORA AND DATABASE COMMANDS

The following commands are useful for creating and manipulating databases in Fedora:

+   `createdb`—Creates a new PostgreSQL database  
+   `createuser`—Creates a new PostgreSQL user account  
+   `dropdb`—Deletes a PostgreSQL database  
+   `dropuser`—Deletes a PostgreSQL user account  
+   `mysql`—Interactively queries the mysqld server  
+   `mysqladmin`—Administers the mysqld server  
+   `mysqldump`—Dumps or backs up MySQL data or tables  
+   `pgaccess`—Accesses a PostgreSQL database server  
+   `pg_ctl`—Controls a PostgreSQL server or queries its status  
+   `psql`—Accesses PostgreSQL via an interactive terminal
# The PostgreSQL Command-Line Client

You invoke the PostgreSQL command-line client with the command psql. Like mysql, psql can be invoked with the name of the database to which you would like to connect. Also like mysql, psql can take several options. These options are listed in Table 21.2.

# TABLE 21.2 Command-Line Options to Use When Invoking psql

| Option | Action |
|---|---|
| -h hostname | Connects to the remote host hostname (if the database server isn't located on the local system). |
| -p n | Specifies the number of the port that the client should connect to. Note that this is a lowercase p. |
| -U username | Connects to the database as the user username. |
| -W | Prompts for a password after connecting to the database. In PostgreSQL 7 and later, password prompting is automatic if the server requests a password after a connection has been established. |
| -? | Displays a help message. |

Several more options are available in addition to those listed in Table 21.2. See the psql's man page for details on all the available options.

# Graphical Clients

If you'd rather interact with a database by using a graphical database client than with the command-line clients discussed in the previous section, you're in luck: A few options are available.

MySQL has an official graphical client, called MySQLGUI. MySQLGUI is available in both source and binary formats from the MySQL website at http://www.mysql.com.

Web-based administration interfaces are also available for MySQL and PostgreSQL. phpMyAdmin and phpPgAdmin are two such products. Both of these products are based on the PHP-embedded scripting language and therefore require you to have PHP installed. Of course, you also need to have a web server installed.
**User Configuration: .my.cnf**
Users who access the database server will have their own configuration file in their home directory: **.my.cnf**. Here the user can specify connection options such as the password used to access the database and the connection timeouts.

```
```plaintext
[client]
password=mypassword

[mysql]
no-auto-rehash
set-variable = connect_timeout=2

[mysql-hotcopy]
interactive-timeout
```
```

# ## Starting and Stopping the MySQL Server

The MySQL server, **mysqld**, can be managed with the `service` command or the `services` tool.

```
```bash
service mysqld start
```
```

The **mysqld** script invokes **safe_mysqld**, which is designed to run MySQL on Unix systems, making sure that data directories are set and log files are running. The **safe_mysqld** script in turn will start up the **mysqld** daemon.

# ## MySQL Tools

MySQL provides a variety of tools (as shown in Table 26-8), including server, client, and administrative tools. Backups can be handled with the **mysqldump** command. The **mysqlshow** command will display a database, just as issuing the SQL command `SELECT *.*` does, and **mysqlimport** can import text files, just like `LOAD INFILE`.

# ## MySQL Management with mysql and mysqladmin

To manage your MySQL database, you use **mysql** as the **root** user. The **mysql** client starts up the MySQL monitor. As the **root** user, you can enter administrative commands to create databases and database tables, add or remove entries, as well as carry out standard client tasks such as displaying data.

| Command | Description |
| :--- | :--- |
| **mysqld** | MySQL server |
| **mysql** | MySQL client |
| **mysqladmin** | Create and administer databases |
| **mysqldump** | Database backup |
| **mysqlimport** | Import text files |
| **mysqlshow** | Display databases |

**TABLE 26-8** MySQL Commands
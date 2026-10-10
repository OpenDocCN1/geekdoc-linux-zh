
# yum install mysql-administrator

If you are familiar with MySQL, you can go ahead and use MySQL Administrator to connect to your MySQL database (assuming it is already running). If MySQL is new to you, I recommend you run through the procedures in this chapter to become familiar with how MySQL works and how to use it from the command line.

To launch the MySQL Administrator window, type **mysql-administrator**. If your MySQL database server is running, as described later in this chapter, enter the server hostname (such as localhost), user name (such as root), and password. The MySQL Administrator window will appear, as shown in Figure 24-1.

![](img/fb202c163797a743c3c6cf236316bc96_950_0.png)

**Figure 24-1:** Connect to your MySQL database using the MySQL Administrator window.

At this point, you can use the MySQL Administrator window to find information about your MySQL server, backup and restore data, or select Catalogs to display information about each database. You can even select the Health option to all kinds of information about activity and usage of your server machine. (If you want to try another MySQL graphical utility, check out the mysql-query-brower package. That tool is made for desigining MySQL tables and running queries.)

## Configuring the MySQL Server

Like most server software in Fedora and RHEL, the MySQL server relies on a startup script and a configuration file to provide the service. Server activities are logged to the **mysqld.log** file in the /var/log directory. There are also **mysql** user and group accounts for managing MySQL activities. The following sections describe how these components all work together.

> **TIP:** For many of the steps described in this section, the MySQL server daemon must be running. Starting the server is described in detail later in this chapter. For the moment, you can start the server temporarily (as root, **type service mysqld start**). Then add a password, as shown in the next section.

### Using mysql user/group accounts

When the MySQL software is installed, it automatically creates a **mysql** user account and a **mysql** group account. These user and group accounts are assigned to MySQL files and activities. In this way, someone can manage the MySQL server without needing to have root permission.

The **mysql** user entry appears in the /etc/passwd file as follows:

```
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
```

The **mysql** entry just shown indicates that both the UID and GID for the **mysql** user are 27. The text string identifying this user account is **MySQL Server**. The home directory is /var/lib/mysql and the default shell is /bin/bash. The home directory identified will contain directories that hold each table of data you define for the MySQL server.

The group entry for **mysql** is even simpler. The following entry in the /etc/group file indicates that the **mysql** group has a group ID (GID) of 27.

```
mysql:x:27:
```

If you care to check the ownership of files associated with MySQL, you will see that most of these files have **mysql** assigned as the user account and group account that own each file. This allows daemon processes that are run by the **mysql** user to access the database files.

### Adding administrative users

To administer MySQL, you need to have at least one administrative account. By default, the root user has full access to your MySQL server database and no password assigned. You can assign a password to the root user using the **mysqladmin** command. To add the root user as a MySQL administrator, log in as the root user and type the following from a Terminal window (substituting your own password in place of *myownpassword*):

```
# mysqladmin -u root password myownpassword
```

After this command is run, the MySQL root user can run any MySQL administrative commands using the password.

MySQL maintains a list of users and passwords that is separate from the list maintained by Fedora. If you don't provide a user name on the command line (as in `-u root` shown above), MySQL assumes you want to use your current Fedora user name to log in to MySQL. However, you will still need to provide the MySQL password (not the Fedora password) for that user to use the MySQL service.

If you want to do MySQL administration, simply add the `-u root` argument to the command line of the MySQL command you are running. The Linux user account has no connection to the MySQL root user account after the MySQL account is created. You would typically use different passwords for the two accounts.

**TIP:** To save yourself the trouble of typing in the password each time you run a MySQL client command, you can add a password option under the [client] group in one of the option files. The most secure way to do that is to create a .my.cnf file in the root user's home directory that can only be accessed by root (chmod 600 /root/.my.cnf) and contains the following lines (Substituting your password for the last argument shown):

```
[client]
password=mypassword
```

## Setting MySQL options

You can set options that affect how the MySQL applications behave by using options files or command-line arguments. The MySQL server (as well as other administrative tools) reads the following options files when it starts up (if those files exist):

- `/etc/my.cnf` — Contains global options read by `mysqld` (server daemon) and `mysql.server` (script to start the server daemon).
- `--defaults-extra-file` — You can identify a file on the command line that contains options to be used by the server. For example, the following command would cause the file /home/jim/my.cnf to be read for options after the global options and before the user-specific options:

```
# mysqld --defaults-extra-file=/home/jim/my.cnf
```

- `$HOME/.my.cnf` — Contains user-specific options. (The $HOME refers to the user's home directory, such as /home/susyj.)

Table 24-1 shows the MySQL commands that read the options files (in the order shown in the previous bullet list) and use those options in their processing. Options are contained within groups that are identified by single words within brackets. Group names that are read by each command are also shown in the table.

Although you can use any of the options files to set your MySQL options, begin by configuring the `/etc/my.cnf` file. Later, if you want to override any of the values set in that file, you can do so using the other options files or command-line arguments.

**Table 24-1: Option Groups Associated with MySQL Commands**

| Command | Description | Group names |
| --- | --- | --- |
| mysqld (in `/usr/libexec`) | The MySQL server daemon | [mysqld] [server] |
| mysqld_safe | Run by the `mysqld` startup script to start the MySQL server | [mysqld] [server] [mysql.server] |
| mysql | Offers a text-based interface for displaying and working with MySQL databases | [mysql] [client] |
| mysqladmin | Used to create and maintain MySQL databases | [mysqladmin] [client] |
| mysamchk | Used to check, fix, and optimize MyISAM databases (.myi suffix) | [mysamchk] |
| myisampack | Used to compress MyISAM database tables | [myisampack] |
| mysqldump | Offers a text-based interface for backing up MySQL databases | [mysqldump] [client] |
| mysqlimport | Loads plain-text data files into MySQL databases | [mysqlimport] [client] |
| mysqlshow | Shows MySQL databases and tables you select | [mysqlshow] [client] |

## Creating the my.cnf configuration file

Global options that affect how the MySQL server and related client programs run are defined in the `/etc/my.cnf` file. The default `my.cnf` file contains only a few settings needed to get a small MySQL configuration going. The following is an example of the `/etc/my.cnf` file that comes with MySQL:

```
[mysqld]
data-dir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
old_passwords=1

[mysql_server]
user=mysql
basedir=/var/lib

[mysql_safe]
err-log=/var/log/mysql.log
pid-file=/var/run/mysql/mysqld.pid
```

Most of the settings in the default my.cnf file define the locations of files and directories needed by the mysqld server. Each option is associated with a particular group, with each group identified by a name in square brackets. The previous options are associated with the mysqld daemon (`[mysqld]`), the MySQL server (`[mysql_server]`), and the *safe_mysqld* script that starts the *mysqld* daemon (`[mysql_safe]`). (Refer to Table 24-1 for a list of these groups.)

The default *datadir* value indicates that `/var/lib/mysql` is the directory that stores the MySQL databases you create. The *socket* option identifies `/var/lib/mysql/mysql.sock` as the socket that is used to create the MySQL communications end-point associated with the *mysqld* server. The *basedir* option identifies `/var/lib` as the base directory in which the *mysql* software is installed. The *user* option identifies *mysql* as the user account that has permission to do administration of the MySQL service. Based on the *old_passwords*=1 value, your MySQL database will use the password format used in previous MySQL 3.x databases.

The *err-log* and *pid-file* options tell the *safe_mysqld* script the locations of the error log (`/var/log/mysql.log`) and the file that stores the process ID of the *mysqld* daemon when it is running (`/var/run/mysql/mysqld.pid`). The *safe_mysqld* script actually starts the *mysqld* daemon from the *mysqld* startup script.

> **NOTE:** Each option that follows a group name is assigned to that group. Group assignments end when a new group begins or when the end of a file is reached.

## Choosing options

Many values are used by the MySQL server that are not explicitly defined in the *my.cnf* file. The easiest way to see which options are available for MySQL server and clients is to run each command with the `--help` option. For example, to view the available *mysqld* options (as well as other information) type the following from a Terminal window:

```
# /usr/libexec/mysqld --verbose --help | less
```

Then press the Spacebar to step through the information one screen at a time. (An example of this output is shown in the next section.)

You can also use the *man* command to find which options are available. For example, to see which options are available to set for the *mysqld* daemon, type the following:

```
man mysqld
```

# Part IV  Networking

TABLE 23-1

Option Groups Associated with MySQL Commands

| Command | Description | Group Names |
| :--- | :--- | :--- |
| mysqld (in /usr/libexec) | The MySQL server daemon | [mysqld] [server] |
| mysqld_safe | Run by the mysqld start-up script to start the MySQL server | [mysql] [server] [mysq1.server] |
| mysql | Offers a command-line interface for displaying and working with MySQL databases. | [mysql] [client] |
| mysqladmin | Used to create and maintain MySQL databases | [mysqladmin] [client] |
| mysamchk | Used to check, fix, and optimize MyISAM databases (_my suffix) | [mysamchk] |
| mysampack | Used to compress MyISAM database tables | [mysampack] |
| mysqldump | Offers a text-based interface for backing up MySQL databases | [mysqldump] [client] |
| mysqlimport | Loads plaintext data files into MySQL databases | [mysqlimport] [client] |
| mysqlshow | Shows MySQL databases and tables you select | [mysqlshow] [client] |

# Creating the my.cnf Configuration File

Global options that affect how the MySQL server and related client programs run are defined in the *etc/my.cnf* file. The default *my.cnf* file contains only a few settings needed to get a small MySQL configuration going. The following is an example of the *etc/my.cnf* file that comes with the *mysql* package from CentOS.

```
[mysqld]
*datadir=/var/lib/mysql
*socket=/var/lib/mysql/mysql.sock
user=mysql

# Default to using old password format for compatibility with mysql 3.x
# clients (those using the mysqlclient10 compatibility package).
old_passwords=1
[mysqld_safe]
*log-error=/var/log/mysqld.log
*pid-file=/var/run/mysqld/mysqld.pid
```
| **Command** | **Description** | **Group names** |
|---|---|---|
| mysqldadmin | Used to create and maintain MySQL databases | [mysqldadmin] [client] |
| myisamchk | Used to check, fix, and optimize MySQL databases (.my1 suffix) | [myisamchk] |
| myisampack | Used to compress MyISAM database tables | [myisampack] |
| mysqldump | Offers a text-based interface for backing up MySQL databases | [mysqldump] [client] |
| mysqlimport | Loads plain-text data files into MySQL databases | [mysqlimport] [client] |
| mysqlshow | Shows MySQL databases and tables you select | [mysqlshow] [client] |

# ### Creating the my.cnf configuration file

Global options that affect how the MySQL server and related client programs run are defined in the `/etc/my.cnf` file. The default `my.cnf` file contains only a few settings needed to get a small MySQL configuration going. The following is an example of the `/etc/my.cnf` file that comes with MySQL:

```
```
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
user=mysql
# Default to using old password format for compatibility with mysql 3.x
# clients (those using the mysqlclient10 compatibility package).
old-password=1

# To allow mysqld to connect to a MySQL Cluster management daemon, uncomment
# these lines and adjust the connectionString as needed.
#ndbcluster
#ndb-connectstring="nodeId=4;host=localhost:1186"

[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid

[ndbd]
# If you are running a MySQL Cluster storage daemon (ndbd) on this machine,
# adjust its connection to the management daemon here.
# Note: ndbd init script requires this to include nodeId:
connect-string="nodeId=2;host=localhost:1186"

[ndb_mgm]
# connection string for MySQL Cluster management tool
connect-string="host=localhost:1186"
```
```
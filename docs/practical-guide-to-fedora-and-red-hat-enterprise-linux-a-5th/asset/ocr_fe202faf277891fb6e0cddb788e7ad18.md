```
# mysql -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.1.39 Source distribution
Type 'help'; or '\h' for help. Type '\c' to clear the current input statement.
mysql> CREATE DATABASE cacti;
Query OK, 1 row affected (0.00 sec)
mysql> GRANT ALL ON cacti.*
-> TO cactiuser@localhost
-> IDENTIFIED BY 'cactipassword';
Query OK, 0 rows affected (0.00 sec)
mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
mysql> exit
Bye
```

Give the following command to set up and populate the database named **cacti**. When MySQL prompts for a password, provide the password for the MySQL user named **root** (not the MySQL user named **cacti**).

```
# mysql -p cacti < /usr/share/doc/cacti®/cacti.sql
Enter password:
```

Most of the information in the `/etc/cacti/db.php` file is correct as installed. Edit this file to change the value assigned to **$database_password** from cactiuser to the same value as **cacti/password** in the preceding step (the password for the MySQL user named **cacti**). Do not change the value assigned to **$database_username**.

```
$database_type = "mysql";
$database_default = "cacti";
$database_hostname = "localhost";
$database_username = "cactiuser";
$database_password = "cactiuser";
$database_port = "3306";
```

# ## CONFIGURING APACHE

Install Apache as explained under “About Apache” on page 842. Modify the **httpd.conf** file as explained on page 845; if you do not make this modification, Apache will display errors when it starts but will work anyway. Run **chktconf** and start the **httpd** daemon. Cacti supplies the content:

The `/etc/httpd/conf.d/cacti.conf` file controls the location and accessibility of Cacti on the Apache server. By default, Cacti is available as **127.0.0.1/cacti** (based on the Alias statement) and only a user on **127.0.0.1** (and not **localhost**: based on the Allow from statement) can access Cacti. The default **cacti.conf** file follows:

```
$ cat /etc/httpd/conf.d/cacti.conf
#
# Cacti: An rrd based graphing tool
```
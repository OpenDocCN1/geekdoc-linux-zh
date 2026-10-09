# PREREQUISITES

Install the following packages:

+   * **mysql-client**
+   * **mysql-server**

When you install the **mysql-server** package, the **dpkg postinst** script displays a pseudographical window that asks you to provide a password for the MySQL user named **root**. This user is not the system **root** user. Provide a password.

Give the following initctl command (page 434) as needed to restart MySQL:

```
$ sudo restart mysql
mysql start/running, process 3433
```

# NOTES

Unlike Oracle, when you create a user, MySQL does not automatically create a database. Under MySQL, users and databases are not as rigidly bound as they are under Oracle.

MySQL has a separate set of users from Linux users. As installed, the name of the MySQL administrator is **root**. Because the MySQL **root** user is not the same as the Linux **root** user, it can have a different password.

# JUMPSTART: SETTING UP MYSQL

MySQL is installed with an anonymous user and the password you supplied for the MySQL user named **root**. For a more secure setup, remove the anonymous user. The **mysql_secure_installation** utility asks a series of questions that allows you to remove the anonymous user and perform other housekeeping tasks. In response to the prompt for the current password for **root**, enter the password you assigned to the MySQL **root** user named **root**. MySQL generates an error when you ask it to remove the test database because Ubuntu does not install this database when you install MySQL.

```
$ /usr/bin/mysql_secure_installation
...
You already have a root password set, so you can safely answer 'n'.
Change the root password? [Y/n] n
... skipping.
...
Remove anonymous users? [Y/n] y
...
Disallow root login remotely? [y/N] y
...
Remove test database and access to it? [y/N] y
- Dropping test database...
ERROR 1008 (HY000) at line 1: Can't drop database 'test'; database doesn't exist
... Failed! Not critical, keep moving...
...
Reload privilege tables now? [y/N] y
...
```
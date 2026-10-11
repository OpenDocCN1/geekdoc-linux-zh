# Tutorial LAMP stack

entry to the IP address. Again, Cloudflare is a good solution for DNS hosting, with an easy-to-use yet advanced toolkit and an extremely short TTL time to live, which means DNS changes effectively take immediate effect. If you ever set waiting for DNS to propagate, you'll appreciate how valuable this feature is!

![](bbox=[0.21, 0.24, 0.56, 0.36])

# 09
Download and install MySQL

Now that you have Apache installed, the next step is to install MySQL — the database engine that is used by most Linux web applications. To install, use the command:

```
$ sudo apt-get install mysql-server mysql-client php-mysql
```

This installs the MySQL server and client (for administration), the Apache module and the PHP module. As part of the install process you'll be prompted to choose a new MySQL root password. Use the sudo mysql_install_db command to complete the installation.

![](bbox=[0.21, 0.52, 0.56, 0.7])

# 10
Secure your installation

After you've installed (and perhaps tested) MySQL, it's a good idea to run the provided script to secure your installation, using the command:

```
$ sudo /usr/bin/mysql_secure_installation
```

This will remove anonymous users, allow you to change the root password to something more secure if required, allow root access only from localhost, and remove the test database. The script will prompt you to reload the privilege tables, which means that the changes will take effect immediately.

# 11
Administering via the command line

As part of the original MySQL installation, you included 'mysql-client', which provides a command-line client for working with your database. For example, to connect to the MySQL database and create a new database, you'd use the command

![](bbox=[0.61, 0.16, 0.92, 0.3])

mysql -u root -p, enter your password when prompted, and then use create database newdbname; and \u newdbname. At this point you could enter SQL statements manually or use \, filename.sql to run a script from disk. Remember to set up non-root accounts as required for your applications.

![](bbox=[0.61, 0.36, 0.92, 0.51])

# 12
Use phpMyAdmin for GUI administration

If administering MySQL from the command line feels like a step too far, or you'd just like something a bit more graphical for viewing your data, then you should consider using phpMyAdmin. It's available from the repositories of most distributions; they are often outdated, however, so it's a better idea to download the latest targz from www.phpmyadmin.net. Installation is as simple as extracting the archive to a web-accessible directory and setting the key values in the config file.

![](bbox=[0.61, 0.63, 0.92, 0.72])

# 13
Back up your data

You are likely to be storing valuable data on your MySQL server, so you should ensure that you make regular backups. The mysqldump command makes it easy to dump the contents of your database to a file, which you can then upload to a remote location (if makes sense to send your /var/www contents up, too, for safe keeping). A number of open source automated backup scripts are available as a starting point, which you can then add to Cron to run on a regular basis.

# 14
Download and install PHP

The final element of the LAMP stack is PHP, the scripting language that powers some of the world's most popular
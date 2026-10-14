
Your MySQL connection id is 250 to server version: 3.23.36

Type 'help;' or '\h' for help. Type '\c' to clear the buffer

mysql>

Now you're ready to start entering SQL commands to build your database. Chapter 24, "Database Server," provides detailed information on creating databases and tables in the MySQL server environment.

## Changing the Root Password

If you want to change the password for the root user account in MySQL, use the mysqladmin command:

```
sudo mysqladmin -p password 'newpassword'
```

The -p parameter causes the mysqladmin program to prompt you for the root user's password. After you type the current password, the mysqladmin program changes the password of the root user account to newpassword.

One of the most frustrating things that can happen to you as the administrator of a LAMP server is forgetting the MySQL root user's password. The root user account in MySQL controls all aspects of the database server. Not being able to log into the MySQL server as the root user means that you can't create new databases or user accounts, or modify existing ones.

Fortunately, there's a trick to recreate the root user account's password if you've forgotten it. Just follow these steps to get things back to normal:

- 1. Stop the MySQL server process. This requires using the mysql script in the /etc/init.d folder:
  sudo /etc/init.d/mysql stop

- 2. Start the MySQL server without using the user tables. MySQL maintains its own set of internal user account tables. You can tell MySQL to start without reading those tables using the command:
  sudo -u mysql mysqld_safe --skip-grant-tables &
  You must start the MySQL server script as the special mysql system user account, and you must use the ampersand symbol (&) at the end to ensure that the MySQL server runs as a background process rather than tying up your command-line session.

- 3. Connect to the MySQL server as the root user without a password. Now that MySQL isn't using the default user tables, you can connect to the server without using a password:
  mysql -u root

- 4. Define a new root password for the root user account. This requires a few lines of SQL code entered at the command-line interface:
  mysql> use mysql;
  mysql> UPDATE user SET password=PASSWORD('newpassword') WHERE user = 'root';
  mysql> flush privileges;
  mysql> exit;
  Note that each SQL statement ends with a semi-colon.

5. Stop, then restart, the MySQL server. For the new password to take effect, you must stop the current MySQL server, then start the server again—this time with the normal start parameters:

```
$ sudo /etc/init.d/mysql stop
$ sudo /etc/init.d/mysql start
```

Because you're starting the MySQL server with the normal start parameters, you can use the standard start script.

6. Log into the MySQL server as the root account with the new password. Use the mysql command-line program with the option to ask for a password:

```
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 250 to server version: 3.23.36

Type 'help;' or '\h' for help. Type '\c' to clear the buffer

mysql>
```

Congratulations! You've successfully recovered from a potential tragedy.

## The phpMyAdmin Tool

An extremely handy tool for managing the MySQL database server via a graphical web interface is the phpMyAdmin tool. The phpMyAdmin tool isn't installed by default in the Ubuntu server installation process, but it is easy to install if your Ubuntu server is connected to the Internet:

- 1. Start a command-line interface prompt on your system.
- 2. Use the apt-get software to retrieve and install phpMyAdmin:
  sudo apt-get install phpmyadmin
  The command retrieves the phpMyAdmin package, along with any dependencies required to install it on your Ubuntu server. During the installation, apt-get provides a dialog box asking which web server to install phpMyAdmin for. Select the apache2 web server option.
- 3. Close the command-line interface.
- 4. Open a browser and navigate to the phpMyAdmin tool. Ubuntu installs the phpMyAdmin tool outside of the document root area of the Apache web server, but it creates an alias pointing to the location. This enables you to connect to the phpMyAdmin tool using the URL:
  http://10.0.0.1/phpmyadmin
  Be sure to use the IP address of your Ubuntu server in the URL.

The first phpMyAdmin tool web page prompts you for a MySQL userID and password to log into the server, as shown in Figure 21-6.
Log in with the root user account, using the password you assigned to it during the Ubuntu server installation. The main phpMyAdmin tool web page showing the databases and the various options available in the tool appear, as shown in Figure 21-7

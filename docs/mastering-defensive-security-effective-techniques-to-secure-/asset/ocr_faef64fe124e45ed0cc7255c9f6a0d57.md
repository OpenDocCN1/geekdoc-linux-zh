+   9. Log in to the database (the password is blank, so just hit Enter when asked), as follows:

```
sudo mysql -u root -p
```

+   10. Now, we need to create a user in the database. In this case, we need to use the same username and password that we just created in the config file (see Figure 12.7). Here's the code you'll need:

+   11. Now, we need to grant all privileges to the user on the database, like this:

```
grant all privileges on dvwa.* to 'user'@'127.0.0.1' identified by 'pass';
```

> Tip\Notice that since we are working on the database, those commands need to end with a semicolon (;).

+   12. Now, the result of those operations on the database should look like this:

```
kali@kali:~~$ sudo mysql -u root -p
Enterter password:
Welcome to the MariaDB monitor. Commands end with ; or \
Your MariaDB connection id is 5
Server version: 10.5.9-MariaDB-1 Debian build-unsigned

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation And others.

Type 'help' or '\h' for help. Type '\c' to clear the current input statement.
MariaDB ([#none]) create user 'dvwa'@'127.0.0.1' identified by 'pass'
Query OK, 0 rows affected (0.001 sec)
MariaDB ([#none]) grant all privileges on dvwa.* to 'dvwa'@'127.0.0.1'
Query OK, 0 rows affected (0.006 sec)
```

Figure 12.7 – Successful creation of the user on the database

+   13. Now is time to navigate to the apache2 directory to configure our Apache server, as follows:

```
cd /etc/php/7.3/apache2
```

+   14. Now, let's modify the php.ini file to ensure the following parameters are on: allow_url_fopen and allow_url_include, as shown in Figure 12.9, and to do that we will use mousepad, as follows:

```
sudo mousepad php.ini
```
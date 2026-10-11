# ### 1.4.2 Preliminary Requirements

To try the examples in this tutorial, a few preliminary requirements must be satisfied:

+   - You must have the MySQL software installed.
+   - You need a MySQL account so that you can connect to the server.
+   - You need a database to work with.

The required software includes the **MySQL** clients and a **MySQL** server. The client programs must be located on the machine where you’ll be working. The server can be located on your machine, although that is not required. As long as you have permission to connect to it, the server can be located anywhere. If you need to get **MySQL**, see Appendix A for instructions. If your network access comes through an Internet service provider (ISP), find out whether the provider offers **MySQL** as a service. If not and your ISP won’t install it, choose a different provider that does offer **MySQL**.

In addition to the **MySQL** software, you’ll need a **MySQL** account so that the server will allow you to connect and create your sample database and its tables. (If you already have a **MySQL** account with the server, you can use that, but you might want to set up a separate account for use with the material in this book.)

At this point, we run into something of a chicken-and-egg problem: In order to set up a **MySQL** account to use for connecting to the server, it’s necessary to connect to the server. Typically, you do this by connecting as the **MySQL** `root` user on the host where the server is running and issuing `CREATE USER` and `GRANT` statements to create a new **MySQL** account and give it database privileges. If you’ve installed **MySQL** on your own machine and the server is running, you can connect to it as `root` and set up a new sample database administrator account with a username of `sampdb` and a password of `secret` as follows (change the name and password to those you want to use, here and throughout the book):

```
```
% mysql -p -u root
Enter password: ******
mysql> CREATE USER 'sampadm'@'localhost' IDENTIFIED BY 'secret';
Query OK, 0 rows affected (0.04 sec)
mysql> GRANT ALL ON sampdb.* TO 'sampadm'@'localhost';
Query OK, 0 rows affected (0.01 sec)
```
```

The `mysql` command includes a `-p` option to cause `mysql` to prompt for the `root` user’s **MySQL** password. Enter the password where you see `******` in the example. I assume that you have already set up a password for the **MySQL** `root` user and that you know what it is. If you haven’t yet assigned a password, just press Enter at the `Enter password:` prompt. However, having no `root` password is insecure and you should assign one as soon as possible. More information on the `CREATE USER` and `GRANT` statements, setting up **MySQL** user accounts, and changing passwords can be found in Chapter 12, “General **MySQL** Administration.”
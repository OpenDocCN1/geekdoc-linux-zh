When you try to make a connection to your MySQL server (or any other MySQL serv- er), the server determines whether a connection should be accepted or refused by check- ing the privilege tables. The following is a brief description of how this works:

+   1. First, the server checks the **user** table to determine whether you should be able to make a connection at all. If an entry exists in the *user* table with the username and corresponding password you entered, and the hostname for this entry is the same as the hostname from which you are connecting, a connection is allowed. The user also gets his/her “global” privileges from the *user* table.
+   2. When you are logged in, the *db* and *host* tables are used to determine whether you are allowed to perform the tasks you try to perform. If no records of the particular user can be found in the *db* or *host* tables, the global privileges from the *user* table are used.

# ## Setting Up Your First MySQL Privileges

Now you are going to use your new knowledge to set up your own privileges. There are two methods of doing this: using GRANT statements or modifying the grant tables directly. Using GRANT statements to modify the privilege system has a few advantages. It is more understandable for human eyes, and it’s also much less error-prone. It’s up to you which method to use.

What you have to do first is connect to the MySQL server as the root user, as follows:

```
```
# mysql -u root -p mysql
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2 to server version: 3.23.4-alpha-log
Type 'help' for help.
mysql>
```
```

# ### Note

Note that if you have given a password for the root account, you have to call mysql with the -p parameter. Otherwise, you will get the following message:

```
```
bash# mysql -u root
ERROR 1045: Access denied for user: 'root@localhost'
(Using password: NO)
```
```

If you don’t give the -p parameter, mysql thinks that you don’t want to enter any password.
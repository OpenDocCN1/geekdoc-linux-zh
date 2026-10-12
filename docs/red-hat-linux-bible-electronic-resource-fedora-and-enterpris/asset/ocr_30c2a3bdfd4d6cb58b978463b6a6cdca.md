The previous example attempts to update the names table (UPDATE names). In this example, each record that has the firstname column set to "Chris" will have the value of the streetaddr column for that record changed to "933 3rd Avenue" instead. Note that the Query found 1 row that matched. That one row matched was also changed, with no error warnings necessary. You can use any combination of values to match records (using WHERE) and change column values (using SET) that you would like. After you have made a change, it is a good idea to display the results to make sure that the change was made as you expected.

To remove an entire row (that is, one record), you can use the DELETE command. For example, if you wanted to delete any row where the value of the firstname column is "Chris", you could type the following:

```
mysql> DELETE FROM names WHERE firstname = "Chris";
Query OK, 1 row affected (0.00 sec)
```

The next time you show the table, there should be no records with the first name Chris.

# ## Adding and Removing User Access

There are several different methods you can use to control user access to your MySQL databases. To begin with, assign a user name and password to every user that accesses your MySQL databases. Then you can use the GRANT and REVOKE commands of mysql to specifically indicate the databases and tables users and host computers can access, as well as the rights they have to those databases and tables.

> > **CAUTION:** Database servers are common targets of attacks from crackers. While this chapter gives some direction for granting access to your MySQL server, you need to provide much more stringent protection for the server if you are allowing Internet access. Refer to the General Security Issues section of the MySQL manual ( `/usr/share/doc/mysql*/manual.html` ) for further information on securing your MySQL server.

# ## Adding users and granting access

Although you have a user account defined to create databases (the root user, in this example), to make a database useful, you may want to allow access to other users as well. The following procedure describes how to grant privileges for your MySQL database to other users.

> > **NOTE:** If you are upgrading your MySQL from a version previous to 3.22, run the `mysql_fix_privilege_tables` script. This script adds new GRANT features to your databases. If you don't run the script, you will be denied access to the databases.

In this example, I am adding a user named bobby that can log in to the MySQL server from the localhost. The password for bobby is 8!yer2shuz. (Remember that there does not have to be a Red Hat Linux user account named bobby. So any user on the localhost with the password for bobby can log in to that MySQL account.)
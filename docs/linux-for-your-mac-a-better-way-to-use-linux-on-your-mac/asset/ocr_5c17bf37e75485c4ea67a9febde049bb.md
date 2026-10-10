# Simple Database Clients

![](bbox=[0.05, 0.05, 0.52, 0.33])

*Figure 12.12*  *Use gnomecard's multiple dialog boxes to enter as much information about your contact as possible.*

For example, the PostgreSQL database system includes 43 different commands and programs used to create and manage one or more databases. The system features user management, access permissions, and graphical shells for queries and reporting.

Another Linux SQL database is MySQL, a database management system with RDBMS features. In this system data is stored in separate files (or tables), then linked to provide data when queried (because of the relational aspect). While MySQL is quite capable of handling large databases (i.e., 50,000,000 records) and integrates well with other computer languages and Web server operations, PostgreSQL is generally given the nod for use in enterprise-class operations on larger computers that provide even larger databases. However, for most users, MySQL should be more than adequate for the task of handling database operations.

Like other services on your Linux system, PostgreSQL and MySQL services and database daemons may be started through initialization scripts under the */etc/rc/init.d* directory. For PostgreSQL, the script is named *postgresql*, MySQL, the script is named *mysql*. The first time you run this script (on a SuSE Linux system), you will see:

```
Creating MySQL privilege database and starting MySQL.
Creating db table
Creating host table
Creating user table
Creating func table
Creating tables_priv table
Creating columns_priv table
...
```
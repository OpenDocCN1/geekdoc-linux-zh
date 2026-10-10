```
mysqladmin -r -O --key_buffer_size=64M *.MYI
```

This would set the key buffer size to 64MB.

# # Summary

MySQL is a structured query language (SQL) database server that runs on Fedora and RHEL, as well as other operating systems. Using a startup script (`/etc/init.d/mysql`) and a configuration file (`/etc/my.cnf`), you can quickly get a MySQL server up and running.

With tools such as the `mysqladmin` and `mysql` commands, you can administer the MySQL server and create databases and tables that are as simple or complex as you need. During `mysql` sessions, you can modify the structure of your database tables or add, update, and delete database records. You have a variety of options for querying data and sorting the output. You also have a lot of control over who can access your database tables and what privileges users have to modify, add to, or delete from the databases you control.
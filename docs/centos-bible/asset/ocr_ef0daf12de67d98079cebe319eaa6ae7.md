The output should show that the user named *steve* is no longer listed as having access to the *all_users* database. (The results might just say "Empty set.")

# ## Backing Up Databases

You can use the *mysqldump* command to back up your MySQL databases. The following command backs up all your MySQL databases:

```
```
# mysqldump -u root -p --opt --all-databases > /home/timothy/all-databases
```
```

In this case, all databases on the local system are copied to the file *all-databases* in the /home/timothy/ directory. You can also use *mysqldump* to back up a single database, several databases, or tables within a database. Refer to the *mysqldump* man page for further information.

# ## Checking and Fixing Databases

Over time, databases can become corrupted or store information inefficiently. MySQL comes with commands that you can use to check and repair your databases. The *mysqlsamlchk* command is available to check MyISAM database tables.

MyISAM tables are used by default with MySQL. (To use a different table type, you can assign it when you first create your MySQL table.) The tables are stored in the directory */var/lib/mysql/dbname* by default, where *dbname* is replaced by the name of the database you are using. For each table, there are three files in this directory. Each file begins with the table name and ends with one of the following three suffixes:

+   * **frm** — Contains the definition (or form) or the table.
+   * **MY** — Contains the table's index.
+   * **MYD** — Contains the table's data.

The following procedure describes how to use the *mysqlsamlchk* command to check your MyISAM tables.

> **WARNING!** Do a backup of your database tables before running a repair with *mysqlsamlchk*. Although *mysqlsamlchk* is unlikely to damage your data, backups are still a good precaution.

+   1. Stop MySQL temporarily by typing the following from a Terminal window as *root* user:

```
```
# /etc/init.d/mysqld stop
```
```
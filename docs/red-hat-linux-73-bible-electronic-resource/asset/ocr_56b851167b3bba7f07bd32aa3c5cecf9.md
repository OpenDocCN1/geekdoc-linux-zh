```
`mysql> SELECT * FROM db WHERE db='allusers';`
```

The output should show that the user named bobby is no longer listed as having access to the allusers database. (The results might just say "Empty set.")

# Checking and Fixing Databases

Over time, databases can become corrupted or store information inefficiently. MySQL comes with commands that you can use to check and repair your databases. The myisamchk and isamchk commands are available to check MyISAM and ISAM database tables, respectively.

MyISAM tables are used by default with MySQL. The tables are stored in the /var/lib/mysql/dbname directory by default, where dbname is replaced by the name of the database you are using. For each table, there are three files in this directory. Each file begins with the table name and ends with one of the following three suffixes:

+   .frm Contains the definition (or form) of the table
+   .YMI Contains the table’s index.
+   .MYD Contains the table’s data.

The following procedure describes how to use the myisamchk command to check your MyISAM tables. (The procedure is the same for checking ISAM tables, except that you use the isamchk command instead.)

> NOTE: Do a backup of your database tables before running a repair with myisamchk. Though myisamchk is unlikely to damage your data, backups are still a good precaution.

+   1. Stop your MySQL server temporarily by typing the following from a Terminal window as the root user:

```
# /etc/init.d/mysql stop
```

+   2. You can check all or some of your database tables at once. The first example shows how to check a table called "names" in the "allusers" database.

```
# myisamchk /var/lib/mysql/allusers/names.MYI
Checking MyISAM file: /var/lib/mysql/allusers/names.MYI
Data records:  5  Deleted blocks:  0
- check file-size
- check key delete-chain
- check record delete-chain
- check index reference
- check record links
```

You could also check tables for all your databases at once as follows:

```
# myisamchk /var/lib/mysql/*/*.MYI
```
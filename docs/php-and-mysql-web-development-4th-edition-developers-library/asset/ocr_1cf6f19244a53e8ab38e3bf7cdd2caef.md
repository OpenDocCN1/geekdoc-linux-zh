# 12.4 Managing MySQL User Accounts

The privileges in Table 12.3 are administrative in nature and, except for GRANT, can be granted only using the ON *.* global-privilege specifier. For example, the RELOAD privilege enables use of FLUSH, so the following statements set up a user named flush that can do nothing but issue FLUSH statements:

```
CREATE USER 'flush'@'localhost' IDENTIFIED BY 'flushpass';
GRANT RELOAD ON *.* TO 'flush'@'localhost';
```

This type of MySQL account can be useful for writing administrative scripts that perform operations such as flushing the logs during log file maintenance (see Section 12.5.7, “Log Management”).

Database-level privileges apply to a particular database and all objects in it. To grant privileges at this level, use an ON db_name.* clause:

```
CREATE USER 'bill'@'racer.snake.net' IDENTIFIED BY 'rock';
GRANT ALL ON sampdb.* TO 'bill'@'racer.snake.net';
```

```
CREATE USER 'reader'@'%' IDENTIFIED BY 'dirt';
GRANT SELECT ON managerie.* TO 'reader'@'%';
```

The first set of statements grants bill full privileges for any table in the sampdb database when he connects from racer.snake.net. The second creates a restricted-access user named reader that can connect from any host to access any table in the managerie database, but only with SELECT statements. That is, reader is a “read-only” user.

You can list multiple privileges to be granted, separated by commas. For example, to give a user the ability to read and modify the contents of existing tables in the sampdb database, but not to create new tables or drop tables, do not grant the ALL privilege for the database. Instead, name only the specific privileges to be enabled:

```
CREATE USER 'jennie'@'%' IDENTIFIED BY 'boron';
GRANT SELECT,INSERT,DELETE,UPDATE ON sampdb.* TO 'jennie'@'%';
```

For more fine-grained access control below the database level, you can grant privileges for individual tables, or even for individual columns in tables. Column-specific privileges are useful when there are parts of a table you want to hide from a user, or when you want a user to be able to modify only particular columns. Suppose that someone volunteers to help you out at the Historical League as an office assistant. That's good news, but you decide to begin by granting your new assistant read-only access to the member table that contains membership information, plus a column-specific UPDATE privilege on the expiration and address-related columns of that table. That way, your assistant will have write access only for the rather modest tasks of updating expiration dates as people renew their memberships and making address changes. The statements needed to set up this MySQL account are as follows:

```
CREATE USER 'assistant'@'localhost' IDENTIFIED BY 'officehelp';
GRANT SELECT, UPDATE (expiration,street,street_city,state,zip)
ON sampdb.member TO 'assistant'@'localhost';
```
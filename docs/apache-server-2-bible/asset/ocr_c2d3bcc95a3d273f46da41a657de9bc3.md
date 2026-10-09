+   3. Change your current database to the newly created auth database using the following command:
+   
+   use auth;

+   4. Now create a table called wwwusers by entering the following lines in the MySQL command prompt.

```
create table wwwusers (
username varchar(40) not null primary key,
passwd varchar(20) not null
);
```

Each row in this table consists of three fields: username, passwd, and groups. The username field is the primary key, which means that MySQL uses this field to index the table, making lookups that use the username very fast. This field is limited to 40 characters. The use of varchar (variable character) instead of fixed char type saves space if usernames are not always 40 characters. The username field cannot be null (that is, empty) because it is also the primary key. The password field is called passwd, which is a maximum of 20 characters long and of the varchar type. It cannot be null.

+   5. Now enter describe wwwusers; command, which should show the following output:

```
mysql> describe wwwusers;
+----+-----+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+----+-----+------+-----+---------+-------+
| username | varchar(40) | | PRI | | |
| passwd | varchar(20) | | | | |
+----+-----+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

This is a verification of the fact the table wwwusers was created as desired.

+   6. Now you need to add user(s) to the table. To add users manually, you need to run the following SQL statement:

```
insert into wwwusers (username , passwd)
values ('user_name',
'user_password');
```

For example:

```
insert into wwwusers (username , passwd)
values ('esmith', 'sale007');
```

Here a user called esmith is added with sale007 as the password in the sales group. Add as many users as you would like. See " Managing Users and Groups in Any RDBM " for details on how to manage users using utility scripts.
# Method 2

```
# mysql -u root mysql
mysql> UPDATE USER SET PASSWORD=PASSWORD("newpassword") where user='root';
mysql> FLUSH PRIVILEGES;    # Use username instead of "root"
mysql> quit
```

# Create user and database (see MySQL doc²⁶)

```
# mysql -u root mysql
mysql> CREATE USER 'bob'@'localhost' IDENTIFIED BY 'pwd';  # create only a user
mysql> CREATE DATABASE bobdb;
mysql> GRANT ALL ON *.* TO 'bob'@'%' IDENTIFIED BY 'pwd';  # Use localhost instead of %
# to restrict the network access
mysql> DROP DATABASE bobdb;                  # Delete database
mysql> DROP USER bob;                        # Delete user
mysql> DELETE FROM mysql.user WHERE user='bob and host='hostname';  # Alt. command
mysql> FLUSH PRIVILEGES;
```

# Grant remote access

Remote access is typically permitted for a database, and not all databases. The file /etc/my.cnf contains the IP address to bind to. Typically comment the line bind-address = out.

```
# mysql -u root mysql
mysql> GRANT ALL ON bobdb.* TO bob@'xxx.xxx.xxx.xxx' IDENTIFIED BY 'PASSWORD';
mysql> REVOKE GRANT OPTION ON foo.* FROM bar@'xxx.xxx.xxx.xxx';
mysql> FLUSH PRIVILEGES;                    # Use 'hostname' or also '%' for full access
```

# Backup and restore

Backup and restore a single database:

```
# mysqldump -u root -psecret --add-drop-database dbname > dbname_sql.dump
# mysql -u root -psecret -D dbname < dbname_sql.dump
```

Backup and restore all databases:

```
# mysqldump -u root -psecret --add-drop-database --all-databases > full.dump
# mysql -u root -psecret < full.dump
```

Here is "secret" the mysql root password, there is no space after -p. When the -p option is used alone (w/o password), the password is asked at the command prompt.

# 18.3 SQLite

SQLite²⁷ is a small powerful self-contained, serverless, zero-configuration SQL database.

# Dump and restore

It can be useful to dump and restore an SQLite database. For example you can edit the dump file to change a column attribute or type and then restore the database. This is easier than messing with SQL commands. Use the command sqlite3 for a 3.x database.

```
# sqlite database.db .dump > dump.sql                # dump
# sqlite database.db < dump.sql                       # restore
```

# Convert 2.x to 3.x database

```
sqlite database_v2.db .dump | sqlite3 database_v3.db
```
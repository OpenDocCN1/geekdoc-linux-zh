If you're running this as a cron job, you might want to precede this command with something such as `mv /usr/local/www/db/PictureArchive.sql /usr/local/www/db/PictureArchive.sql-old` and then a semicolon. This will move the old dump file out of the way so the new dump file can be created. Then it will run the dump, all in one command.

If you want to quickly make a snapshot of the entire database directory without creating a dump file, you can use `mysqlhotcopy`. This is a Perl script that locks the tables and copies all their associated files into a new specified location; if your database becomes corrupted or lost, you can simply shut down MySQL, move the files into their appropriate locations under `/var/db/mysql`, and restart the server. To run `mysqlhotcopy`, do the following:

```
```
mysqlhotcopy --user="frank" --password="frank's password" PictureArchive 
/​usr/local/www/db/PictureArchive
```
```

As for PostgreSQL, the `pgdump` command is the equivalent of `mysqlhotcopy`. It is easiest to run `pgdump` as the `pgsql` user who owns the database; create `pgsql`'s crontab file with crontab -u pgsql:

```
```
pgsql PictureArchive > /usr/local/www/db/PictureArchive.sql
```
```

# ## Restoring the Database

Restoring from a `.sql` file output from `mysqldump` or `pgdump` is conceptually very simple. It's just a “replay” of SQL commands, which theoretically will re-create the entire database in every detail—first by rebuilding the tables and all their indexes and then by reinserting all the data.

To restore a MySQL database from a `.sql` file, you must first create the database (if it has been deleted or dropped) and then use the following command:

```
```
mysql -p PictureArchive < /usr/local/www/db/PictureArchive.sql
```
```

You will be prompted for your password. (Alternatively, you can specify the `frank` user with `-u` or `--user=`, and Frank's password with `-p` or `--password=`, as you saw earlier in this chapter.) After this is accepted, the `.sql` file will be read into the database, and through the use of `SHOW TABLES` and a few `DESCRIBE <table>` and `SELECT` queries, you should be able to verify that everything has been properly restored.

The process is almost exactly the same in PostgreSQL. First, use `su` to change to the `pgsql` user; then create the database (using `createdb`, as you saw earlier) if it doesn't already exist. Then start `psql`, reading in the `.sql` file:

```
```
psql < /usr/local/www/db/PictureArchive.sql
```
```

If all goes well, you should be back up and running.
copying template1 to template0... ok

Success. You can now start the database server using:

```
```bash
/usr/bin/postmaster -D /usr/local/pgsql/data
or
/usr/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
```
```

This initializes the database and sets the permissions on the data directory to their correct values.

> **CAUTION**
> 
> The initdb program sets the permissions on the data directory to 700. You should not change these permissions to anything else to avoid creating a security hole.

You can start the postmaster program with the following command (make sure you are still the user postgres):

```
```bash
$ postmaster -D /usr/local/pgsql/data &
```
```

If you have decided to use a directory other than /usr/local/pgsql/data as the data directory, you should replace the directory in the postmaster command line with whatever directory you are using.

> **TIP**
> 
> By default, Ubuntu makes the PostgreSQL data directory /var/lib/pgsql/data. This isn't a very good place to store the data, however, because most people do not have the necessary space in the /var partition for any kind of serious data storage. Note that if you do change the data directory to something else (such as /usr/local/pgsql/data, as in the examples in this section), you need to edit the PostgreSQL startup file (named postgres) located in /etc/init.d to reflect the change.

# Creating a Database in PostgreSQL

Creating a database in PostgreSQL is straightforward, but it must be performed by a user who has permissions to create databases in PostgreSQL—for example, initially the user named postgres. You can then simply issue the following command from the shell prompt (not the PSQL client prompt, but a normal shell prompt):

```
```bash
# su - postgres
-bash-2.05b$ createdb database
```
```

where database is the name of the database you want to create.
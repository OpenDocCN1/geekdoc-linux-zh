The user foobar can now connect to the database sampledata by using the password secretword, and foobar has all privileges on the database, including the ability to create and destroy tables. For example, the user foobar can now log in to the server (by using the current hostname—shuttle2, in this example), and access the database like so:

```
```text
$ mysql -h shuttle2 -u foobar -p animals
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \\g.
Your MySQL connection id is 43 to server version: 3.23.58

Type 'help;' or '\\h' for help. Type '\\c' to clear the buffer.

mysql>
```
```

> **NOTE:**

See the section “The MySQL Command-Line Client” for additional command-line options.

Later, if you need to revoke privileges from foobar, you can use the REVOKE statement. For example, the following statement revokes all privileges from the user foobar:

```
```sql
REVOKE ALL ON animals FROM foobar;
```
```

Advanced database administration, privileges, and security are very complex topics that are beyond the scope of this book. See the section “Reference” at the end of this chapter for links to online documentation. You can also check out Luke Welling’s and Laura Thomson’s book *PHP and MySQL Development* from Sams Publishing.

# Configuring PostgreSQL

If you do not want to use the version of PostgreSQL bundled with Ubuntu, the latest PostgreSQL binary files and source are available at http://www.postgresql.org. The PostgreSQL packages are distributed as several files. At a minimum, you probably want the postgresql, postgresql-server, and postgresql-libs packages. You should see the README file in the FTP directory ftp://ftp.postgresql.org/pub/ to determine whether you need any other packages.

If you are installing from the Ubuntu package files, a necessary postgres user account (that is, an account with the name of the user running the server on your system) is created for you automatically:

```
```text
$ fgrep postgres /etc/passwd
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
```
```

Otherwise, you need to create a user called postgres during the installation. This user shouldn’t have login privileges because only root should be able to su to become this
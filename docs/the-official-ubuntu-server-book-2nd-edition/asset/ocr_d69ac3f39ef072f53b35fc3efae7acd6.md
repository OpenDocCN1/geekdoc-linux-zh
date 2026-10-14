# PostgreSQL

PostgreSQL and MySQL are the yin and yang of the open source database world. Whereas MySQL focused on speed and ease of use early on and then started to add more advanced database features, PostgreSQL focused on advanced database features first and then worked on optimization and ease of use. Both databases have their following, and all of the major open source database-backed Web software supports both databases. PostgreSQL moves far beyond Web site databases, though, with an advanced feature set including full ACID compliance, foreign keys, joins, views, triggers, and stored procedures.

# Install PostgreSQL

Even though MySQL has the reputation of ease of use, PostgreSQL under Ubuntu is also simple to install and use. To install PostgreSQL, you can either select PostgreSQL Server as you install Ubuntu or afterward with tasksel, or you can use a package manager to install the postgresql package:

```
$ sudo apt-get install postgresql
```

Once the postgresql package has been installed, the database service will start in the background and you can then set up your superuser account and create a database. The initial administration will be performed by the postgres user, so first use sudo to become that user:

```
$ sudo -u postgres -s
```

Now from this shell you can create a new user account. You can choose to maintain the postgres user as the main superuser and then control who can become that user with sudo, or alternatively you can set up a new database user with superuser privileges. If I wanted to create a new superuser on my PostgreSQL database with the username kyle, I just need to pass the right flags to the createuser program:

```
$ createuser -P -s -e kyle
Enter password for new role:
Enter it again:
CREATE ROLE kyle PASSWORD 'md56966c432c869202883876a8b4f925ccc' SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN;
```
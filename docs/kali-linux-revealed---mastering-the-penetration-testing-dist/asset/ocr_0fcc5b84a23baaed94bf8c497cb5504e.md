Depending on how they connect, clients are authenticated in different ways. The pg_hba.conf configuration file defines who is allowed to connect on each socket and how they are authenticated. By default, connections on the file-based socket use the Unix user account as the name of the PostgreSQL user, and it assumes that no further authentication is required. The TCP connection requires the user to authenticate with a username and a password (though not a Unix username/password rather than one by PostgreSQL itself).

The postgres user is special and has full administrative privileges over all databases. We will use this identity to create new users and new databases.

# Creating Users and Databases

The createuser command adds a new user and dropdb removes one. Likewise, the createdb command adds a new database and removes one. Each of these commands have their own manual pages but we will discuss some of the options here. Each command on the default cluster (running on port 5432) you can use --port to modify acts and databases of an alternate cluster.

These commands must connect to the PostgreSQL server to do their job and must be authenticated as a user with sufficient privileges to execute the specific operation. The easiest way to achieve this is to use the postgres Unix account and connect over the file-based socket:

```
# su - postgres
$ createuser -P king_phisher
Enter password for new role:
Enter it again:
$ createdb -T template0 -E UTF-8 -O king_phisher king_phisher
$ exit
```

In the example above, the -P option asks to query for a password once it creates the new king_phisher user. Looking at the createdb command, the -O defines the user owning the new database (which will have full rights to create tables and grant permissions and so on). We also want to be Unicode strings, so we add the -E UTF-8 option to set the encoding, which in turn requires us to use the -T to pick another database template.
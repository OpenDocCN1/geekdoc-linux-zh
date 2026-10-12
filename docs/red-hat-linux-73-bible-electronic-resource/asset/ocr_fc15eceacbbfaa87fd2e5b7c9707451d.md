> TIP: For many of the steps described in this section, the MySQL server daemon must be running. Starting the server is described in detail later in this chapter. For the moment, you can start the server temporarily by typing the following: /etc/init.d/mysqld start

# Using mysql user/group accounts

When the MySQL software is installed, it automatically creates a mysql user and a mysql group. These user and group accounts are assigned to MySQL files and activities. In this way, someone can manage the MySQL server without needing to have root permission for the computer.

The mysql user entry appears in the /etc/password file as follows:

```
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
```

The mysql entry just shown indicates that the UID and GID for the mysql user is 27. The text string identifying this user account is "MySQL Server." The home directory is /var/lib/mysql and the default shell used by the user is /bin/bash. The home directory identified will contain directories that hold each table of data you define for the MySQL server.

The group entry for mysql is even simpler. The following entry in the /etc/group file indicates that the mysql group has a group ID (GID) of 27.

```
mysql:x:27:
```

If you care to check the ownership of files associated with MySQL, you will see that most of these files have mysql assigned as the user account and group account that own each file. This allows daemon processes that are run by the mysql user to access the database files.

# Adding administrative users

To administer MySQL, you need to create at least one administrative account. You can do this using the mysqladmin command. To add the root user as a MySQL administrator, log in as the root user and type the following from a Terminal window:

```
# mysqladmin -u root password my47gmc
```

You want to enter your own password instead of the my47gmc shown above. After this command is run, the root user can run any of the MySQL administrative commands by typing the password when prompted.

If you happen to be logged in as another user when you want to use administrative privilege for a MySQL command, you can do that without re-logging in. Simply add the argument -u root to the command line of the MySQL command you are running. In other words, the Linux root user account has no connection to the MySQL root user account once the MySQL account is created. You would typically use different passwords for the two accounts.
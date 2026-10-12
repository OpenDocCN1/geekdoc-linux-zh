activities. In this way, someone can manage the MySQL server without needing to have root permission.

The `mysql` user entry appears in the `/etc/passwd` file as follows:

```
```bash
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
```
```

The `mysql` entry just shown indicates that both the UID and GID for the `mysql` user are 27. The text string identifying this user account is MySQL Server. The home directory is `/var/lib/mysql` and the default shell is `/bin/bash`. The home directory identified will contain directories that hold each table of data you define for the MySQL server.

The group entry for `mysql` is even simpler. The following entry in the `/etc/group` file indicates that the `mysql` group has a group ID (GID) of 27.

```
```bash
mysql:x:27:
```
```

If you care to check the ownership of files associated with MySQL, you will see that most of these files have `mysql` assigned as the user account and group account that own each file. This allows daemon processes that are run by the `mysql` user to access the database files.

# # Adding administrative users

To administer MySQL, you need to have at least one administrative account. By default, the root user has full access to your MySQL server database and no password assigned. You can assign a password to the root user using the `mysqladmin` command. To add the root user as a MySQL administrator, log in as the root user and type the following from a Terminal window (substituting your own password in place of my47gmc):

```
```bash
# mysqladmin -u root password my47gmc
```
```

After this command is run, the root user can run any MySQL administrative commands using the password.

If you happen to be logged in as another user when you want to use administrative privilege for a MySQL command, you can do that without re-logging in. Simply add the `-u root` argument to the command line of the MySQL command you are running. In other words, the Linux root user account has no connection to the MySQL root user account after the MySQL account is created. You would typically use different passwords for the two accounts.

> **TIP:** To save yourself the trouble of typing in the password each time you run a MySQL client command, you can add a password option under the `[client]` group in one of the option files. The most secure way to do that is to create a `.my.cnf` file in the root user's home directory that contains the following lines (substituting your password for the last argument shown):
> 
> ```ini
> [client]
> password=my47gmc
> ```
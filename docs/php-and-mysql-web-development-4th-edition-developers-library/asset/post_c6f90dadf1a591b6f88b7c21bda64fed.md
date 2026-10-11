
## A.4 Installing MySQL on Unix

A directory located under the MySQL installation directory. Your shell uses this variable to determine where to look for commands. PATH usually is set in one of your shell’s startup files, such as .tcshrc for csh, or .bashrc or .bash_profile for bash. For example, if you use tcsh, there might be a line in your .tcshrc file that looks like this:

```
setenv PATH /bin:/usr/bin:/usr/local/bin
```

If the MySQL client programs are installed in /usr/local/mysql/bin, change the value of PATH as follows:

```
setenv PATH /usr/local/mysql/bin:/bin:/usr/bin:/usr/local/bin
```

If you use bash, one or more of your shell startup files might contain a line like this:

```
PATH=/bin:/usr/bin:/usr/local/bin
```

Change the setting to this:

```
PATH=/usr/local/mysql/bin:/bin:/usr/bin:/usr/local/bin
```

After you modify the shell startup file or files, the new setting takes effect each time you log in thereafter.

### A.4.3.2 Initializing the Data Directory and Grant Tables

Before you can use your MySQL installation, you must initialize the mysql database that contains the grant tables controlling network access to your server. This step is needed only for a first-time installation and only if you will run a server. It is not needed for an upgrade to an existing installation or for a client-only installation.

In the following instructions, DATADIR represents the pathname to your data directory. It is typically located under your MySQL installation base directory and named data or var. Normally, you run the commands shown here as root. If you’re logged in as the MySQL user (for example, mysql) or you’ve installed MySQL under your own account because you intend to run it for yourself, you can execute the commands without being root and should omit the --user option. You can also skip the chown and chgrp commands.

To initialize the data directory, the mysql database, and the default grant tables, change location into the MySQL installation directory and run the mysql_install_db script. (You need not do this if you are installing from RPM packages or a Mac OS X package because they run mysql_install_db for you.) For example, if you installed MySQL into /usr/local/mysql, the commands look like this:

```
# cd /usr/local/mysql
# bin/mysql_install_db --user=mysql
```

If mysql_install_db fails, consult the installation chapter in the MySQL Reference Manual to see what it says about the problem you’re encountering. If mysql_install_db doesn’t run to completion successfully, any grant tables it may have created are likely incomplete. You should remove them because mysql_install_db does not try to re-create any tables that it finds already created. You can remove the entire mysql database like this:

```
# rm -rf DATADIR/mysql
```

After running `mysql_install_db`, change the user and group ownership and the access mode of all files under the data directory. Assuming that the user and group names both should be `mysql`, the commands look like this:

```
# chown -R mysql DATADIR
# chgrp -R mysql DATADIR
# chmod -R go-rwx DATADIR
```

The `chown` and `chgrp` commands change the ownership to the MySQL login account user and group, and `chmod` changes the access mode to keep everybody out of the data directory except that user.

### A.4.3.3 Starting the Server

This step is needed only if you plan to run a server. Skip it for a client-only installation. Run the commands in this section from the MySQL installation directory (just as for the commands in the previous section). Normally, you run the commands as `root`. If you're logged in as the MySQL user (for example, `mysql`) or you’ve installed MySQL under your own account, you can execute the commands without being `root` and should omit the `--user` option.

Change location into the MySQL installation base directory (for example, `/usr/local/mysql`), and then use the following command to start the server:

```
# cd /usr/local/mysql
# bin/mysql_safe --user=mysql &
```

The `--user` option tells the server to run as `mysql`.

If you are installing MySQL for the first time on this machine, there are other actions that you'll probably want to perform at this point:

- The default installation enables anyone to use the MySQL `root` accounts without a password. For security reasons, it’s a good idea to assign passwords to them.
- You can arrange for the server to start and stop automatically as part of your system’s normal startup and shutdown procedures.
- You can put the `--user` option in an option file to avoid having to specify it each time you start the server.
- Various kinds of logging can be enabled. These are useful for monitoring the server, for replication, and for data recovery procedures.
- You can enable or disable storage engines, or specify tuning parameters for them.

Instructions for performing these actions are given in Chapter 12.

### A.4.3.4 Installing or Upgrading Additional System Tables

If you are upgrading a MySQL installation, it is possible that the grant table structure has changed since your original installation. To update the tables to the current structure, use the instructions in Section 12.4, “Managing MySQL User Accounts.”

To set up the time zone tables that are needed for named time zone support, use the instructions in Section 12.9.1, “Configuring Time Zone Support.”

The `mysql` command-line client can access server-side help via the `help` command. For this to work, the help tables in the `mysql` database must be set up. Most installation methods do this automatically for a first-time install, but if you use a method for which this does not occur, you can load the help tables manually. To do this, make sure that the server is running. Then locate the `fill_help_tables.sql` file, which contains SQL statements that create and load the tables. Likely locations are in `/usr/share/mysql`, the `share` directory under the MySQL base installation directory, or the `scripts` directory of a source distribution. After you find the file, execute the following command in the directory where the file is located:

```
mysql -p -u root mysql < fill_help_tables.sql
```

The command will prompt you for the `root` account password. Omit the `-p` option if you have not yet set up a password.

## A.4.4 Installing Perl DBI Support on Unix

Install the DBI software if you want to write Perl scripts that access MySQL databases:

- You must install the DBI module that provides the general DBI driver, and the `DBD:mysql` module that provides the MySQL-specific driver. DBI requires Perl 5.6.0 or later. (If you don’t have Perl installed, visit http://www.perl.com/ , download a Perl distribution, and install it before you install DBI support.)
- The MySQL C client libraries and header files must be available as well, because `DBD:mysql` uses them. They should already have been installed as part of the MySQL installation procedure.
- If you want to write Web-based DBI scripts, install the CGI.pm module.

To find out whether a given Perl module already is installed, use the `perldoc` command. If the module is installed, `perldoc` will display its documentation:

```
% perldoc DBI
% perldoc DBD::mysql
% perldoc CGI
```

The easiest way to install Perl modules under Unix is to use the CPAN shell. Issue the following commands as `root`:

```
# perl -MCPAN -e shell
cpan> install DBI
cpan> force install DBD::mysql
cpan> install CGI
```

The installation command for `DBD:mysql` uses `force install` to cause installation to proceed even if the test phase fails. The tests assume that they can connect to a server running on the local host using an anonymous-user MySQL account with no password. This means the tests fail unless you happen to have an insecure account. (If you do have such an account, the tests should succeed and you can omit `force`, but you really should assign passwords to all your MySQL accounts.)

Another way to install Perl modules is to download source distributions from cpan.perl.org as compressed `tar` files. Unpack a distribution file *dist_file*.tar.gz using one of the following commands (use the second command if your version of `tar` doesn't understand the `z` option):

```
% tar zxf dist_file.tar.gz
% gunzip < dist_file.tar.gz | tar xf -
```

Then change location into the distribution directory created by the `tar` command and run these commands (you might need to be `root` to run the installation step):

```
% perl Makefile.PL
% make
% make test
% make install
```

The `make test` command will fail unless you have an insecure anonymous-user MySQL account, as described earlier in this section. If you want to use a different account, run `perl Makefile.PL --help` to see how. Otherwise, just ignore failed tests and proceed to the installation command.

If you have problems installing the Perl modules, consult the `README` file for the relevant distribution, as well as the mail archives for the DBI mailing list. The answers for most installation problems can be found there.

## A.4.5 Installing Apache and PHP on Unix

The PDO database-access extension for PHP requires PHP 5.0 or higher. For PHP 5.1 or higher, PDO is included with PHP. For PHP 5.0, PDO must be installed separately; this can be done using the `pecl` command-line program. See http://www.php.net/pdo for more information.

The following instructions assume that you'll run PHP as a dynamic shared object (DSO) module using the Apache `httpd` server. This means that Apache should be installed first, and then you can build and install PHP. If Apache is not installed on your system already, you can either install a binary distribution that has DSO support enabled, or else compile a source distribution to include DSO support.

After Apache has been installed, configure your PHP distribution using a command such as the one following (enter it on a single line). The command assumes that Apache and MySQL are installed under /usr/local. Adjust the pathname as necessary for your system.

```
% ./configure --with-apxs=/usr/local/apache/bin/apxs --enable-pdo --with-pdo-mysql=/usr/local/mysql
```

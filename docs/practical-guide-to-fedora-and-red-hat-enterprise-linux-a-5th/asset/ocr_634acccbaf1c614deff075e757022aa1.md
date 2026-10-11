```
# yum groupinfo "MySQL Database"
Loaded plugins: presto, refresh-packagekit
Setting up Group Process
Group: MySQL Database
Description: This package group contains packages useful for use with MySQL.
Mandatory Packages:
  mysql
Default Packages:
  MySQL-python
  libdbi-dbd-mysql
  mysql-connector-odbc
  mysql-server
  perl-DBD-MySQL
  unixODBC
Optional Packages:
  mod_auth_mysql
  mysql-bench
  mysql-devel
  mysqlreport
  mysqltuner
  php-mysql
  qt-mysql
  qt3-MySQL
```

To install a group of packages, give the command **yum groupinstall** followed by the name of the group.

# Other yum Commands

Many yum commands and options are available. A few of the more useful commands are described here. The yum man page contains a complete list.

+   *   **check-update** Lists packages that are installed on the local system and have updates available in the yum repositories.
+   *   **clean all** Removes header files that yum uses for resolving dependencies. Also removes cached packages—yum does not automatically remove package once they have been downloaded and installed, unless you set **keepcache** to 0.
+   *   **clean metadata** Removes the files that yum uses to determine remote package availability. Using this option forces yum to download all metadata the next time you run it.
+   *   **list available** Lists all packages that can be installed from the yum repositories.
+   *   **search _word_** Searches for _word_ in the package description, summary, packager, and name.

# yum-updatesd: Runs yum Automatically

The **yum-updatesd** daemon notifies you when updates are available for the local system; it is turned on by default. This daemon is configured with the */etc/yum/yum-updatesd.conf* file. Use **service** (page 427) and **chkconfig** (page 429) to set up and turn on/off this daemon. The log is kept in */var/log/yum.log* or in the location specified in the configuration file.
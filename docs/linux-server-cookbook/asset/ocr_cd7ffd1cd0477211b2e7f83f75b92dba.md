Removes privileges for a user or role. The simplified syntax is indicated in the following code:

```
REVOKE privilege ON object_type FROM user_or_rolenitu
```

For example, to remove the privilege previously assigned to *GRANT*, the following statement will perform the action:

```
**REVOKE ALL PRIVILEGES** ON school.* **FROM** 'agonzalez@'localhost';
```

# ### MariaDB server

For the installation of the **MariaDB server**, it is required to install the package **mariadb-server**, available in all the popular Linux distributions available. The installation in a Ubuntu and Debian derivatives distributions will start the service and enable it to be started on boot automatically. The name of the service is **mariadb.service**. Red Hat Enterprise Linux distribution and derivatives require to be started and enabled using the command **systemctl**.

It is important to have into consideration that **MariaDB** is a fork of **MySQL**, and some commands and configuration files are interchangeable. For example, the service path */usr/sbin/mysqld* is a link to the binary file */usr/sbin/mariadbd*.

The main configuration for the service is the file *my.cnf*. The location varies depending on the Linux distribution used:

+   - *Ubuntu, Debian*, and derivatives: Inside of the directory */etc/mysql/*. This file is a link to the file */etc/alternatives/my.cnf*, which at the same time, is a link to file */etc/mysql/mariadb.cnf*.

+   - Red Hat Enterprise Linux and derivatives: The file is inside the directory */etc/*.

The file *my.cnf* is an entry point configuration used to indicate the directories with the global configurations for the service. The following code shows the content of *my.cnf* in a Ubuntu server:

```
[client-server]
socket = /run/mysqld/mysqld.sock
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/
```
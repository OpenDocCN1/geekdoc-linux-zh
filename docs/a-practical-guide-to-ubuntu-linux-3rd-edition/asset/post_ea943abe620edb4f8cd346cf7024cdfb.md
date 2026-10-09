
- Periodically polls tracked devices for data. The tool most commonly used to collect this data is SNMP (Simple Network Management Protocol; www.net-snmp.org).
- Stores the data in an RRD file.
- Has a Web interface that allows you to examine graphs generated from the stored data. These graphs typically display daily, weekly, monthly, and yearly information.

Cacti’s configuration is performed through its Web interface, whereas MRTG and Criket are configured by editing text files.

RRD files and RRDtool are the key to much of Cacti’s functionality. The Cacti Web site describes Cacti as “the complete RRDtool-based graphing solution.” RRD files store time-series data efficiently and, through the use of aggregation functions, make it easy to keep a lot of detail for recent time periods but progressively less detail as the data in the files ages. RRDtool easily generates both simple and complex graphs from RRD files.

Many extensions and plugins are available for Cacti. Once you are familiar with the basic use and operation of Cacti, visit cacti.net/additional_scripts.php for a partial list of these additions. Also visit the documentation and the user forums to obtain more information about Cacti and to learn how you can add functionality and support for different devices and data sources.

## Configuring SNMP

If you want to monitor data sources on the local system, install and run the SNMP daemon on the local system as explained under “Setting Up a Remote Data Source” on page 654.

## Setting Up LAMP

Cacti is a LAMP (Linux, Apache, MySQL, PHP) application; you must install and configure these applications before you can configure Cacti. This section explains how to set up the software on the system running Cacti. See “Setting Up a Remote Data Source” on page 654 for an explanation of how to set up a system that Cacti will query and report on. By default, Cacti sets up the local system to run Cacti and be a data source.

## Notes

When you set up LAMP, you use the MySQL databases named `mysql` and `cacti`. Ubuntu sets up the `mysql` database when you install MySQL. You set up and populate the `cacti` database as explained under “Configuring MySQL” on page 650.

You need to set up the following database users. Each of these accounts should have a password:

- A user named **root** for the database named **mysql**. This user must be named root. The MySQL installation script sets up this user and prompts for a password.
- A user named **cactiuser** for the database named **mysql**. You can change this username, but as installed, Cacti is set up to use **cactiuser**.
- A Cacti administrative user for the database named **cacti**. As set up when you install Cacti, this user has the name **admin** and the password **admin**. You can set up additional Cacti user accounts.

As of this writing, Ubuntu 10.04 has Cacti 0.8.7e-2 in its repositories. Do not be misled by the pre-1.0 version number: Cacti is stable and in use on many systems.

## PREREQUISITES

Install the following packages:

- cacti
- mysql-client (page 628)
- mysql-server (page 628)
- php5-cli
- apache2 (Apache; page 899)
- rrdtool
- snmp

When you install the cacti package, APT installs all packages necessary to run Cacti. It also runs the MySQL installation script (page 629) and asks if you want to run the Cacti installation script.

During installation, the MySQL installation script displays a pseudographical window that includes the following prompt:

```
New password for the MySQL "root" user:
```

Respond to this prompt with the password for the **mysql** database user named **root** and click **OK**. The script prompts you to reenter the password.

Next the PHP installation script displays a message (which you can ignore) about the location of **libphp-adodb**.

The next pseudographical window asks which Web server you want Cacti to use. Select **Apache2**. After installing some packages, the Cacti installation script asks if you want to use **dbconfig-common** to configure the database for Cacti. Respond with **No**. As of this writing the script did not work; the next sections explain how to configure the Cacti database manually.

**Firewall** The `snmpd` daemon, which runs on systems monitored by Cacti, uses UDP port 161. If the monitored system is running a *firewall*, you need to open this port (page 876). If you want to work with Cacti from a browser on a system other than the one running Cacti, you need to open TCP port 80 on the system running Cacti (refer to “Firewall” on page 901). For more general information, see Chapter 25, which details the *iptables* utility.

## CONFIGURING MYSQL

For a more secure installation, run `mysql_secure_installation` as explained under “JumpStart: Setting Up MySQL” on page 629.

### Two databases, two users: the cactiuser in the mysql database and the admin user in the cacti database

**caution** Do not confuse the databases and users.

The **mysql** database has a user named **cactiuser**. This user sets up and administrates the **cacti** database using MySQL. You assign a password to this user when you set up the **cacti** database.

The **cacti** database has a user named **admin**. Cacti sets up this user when you populate the **cacti** database using the `cacti.sql` script. It automatically assigns the password **admin** to this user, but then requires you to change the password when you first log in on Cacti.

**Create the cacti database** Issue the following commands to create a database named **cacti**, create a **mysql** database user named **cactiuser**, grant that user the necessary privileges, and assign a password to that user. Replace `cacti_password` in the following example with your choice of a password. Although the FLUSH PRIVILEGES statement is not required, it is good practice to include it.

```
$ sudo mysql -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.1.41-3ubuntu2.1 (Ubuntu)
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CREATE DATABASE cacti;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL ON cacti.*
    -> TO cactiuser@localhost
    -> IDENTIFIED BY 'cacti_password';
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

mysql> exit
Bye
```

**Set up and populate the cacti database** Give the following commands to set up and populate the database named **cacti**. When MySQL prompts for a password, provide the password for the MySQL user named **root** (not the MySQL user named **cactiuser**).

```
$ zcat /usr/share/doc/cacti/cacti.sql.gz > cacti.sql
$ sudo -s mysql -p cacti < cacti.sql
Enter password:
$ rm cacti.sql
```

**Edit debian.php**

Working with root privileges, edit the /etc/cacti/debian.php file so that it looks like the following example. Assign cactiuser to $Database_username, assign the value of cacti_password from the preceding step to $Database_password (the password for the mysql database user named cactiuser), and assign cacti to $Database_default. Do not change any other values.

```
$Database_username='cactiuser';
$Database_password='cacti_password';
$basepath='';
$Database_default='cacti';
$Database_hostname='';
$Database_port='';
$dbtype='mysql';
```

## CONFIGURING APACHE

After Apache is installed, modify the configuration files as explained on page 903; if you do not make these modifications, Apache will display errors when it starts but will work anyway. Use the apache2 init script to restart the httpd daemon (page 902). Cacti supplies the content.

The /etc/cacti/apache.conf file controls the location and accessibility of Cacti on the Apache server. You do not have to modify this file. By default, Cacti is available as localhost/cacti or, from a remote system, as IP/cacti, where IP is the IP address of the system running Cacti. The default cacti.conf file follows:

```
$ cat /etc/cacti/apache.conf
Alias /cacti /usr/share/cacti/site

<DirectoryMatch "/usr/share/cacti/site">
Options +FollowSymLinks
AllowOverride None
order allow,deny
allow from all

AddType application/x-httpd-php .php

php_flag magic_quotes_gpc Off
php_flag short_open_tag On
php_flag register_globals Off
php_flag register_argc_argv On
php_flag track_vars On
# this setting is necessary for some locales
php_value mbstring.func_overload 0
php_value include_path .

DirectoryIndex index.php
</DirectoryMatch>
```

See “Alias” (page 923) and “Allow” (page 930) for more information.

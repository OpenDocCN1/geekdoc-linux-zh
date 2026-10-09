
By default, SELinux will not allow you to share your home directory. Use `system-config-selinux` (page 475) to activate the `samba_enable_home_dirs` Boolean if you want to allow sharing. Any Windows or Mac user can access this share, which can be used to exchange files between users and among Linux, Mac, and Windows systems.

## INTRODUCTION TO CACTI

Cacti (cacti.net) is a network monitoring tool that graphs system and network information over time (*time-series data*) and provides a comprehensive Web interface for browsing and examining the ongoing performance of the devices on a network.

For example, Cacti can monitor the network traffic passing through the network ports on local servers and the switch and router ports on the local network. Cacti graphs provide information on traffic levels on the various parts of the network. When the network is slow, for example, you can refer to the historical graphs and see if anything out of the ordinary has occurred. In addition to network traffic levels, Cacti can collect data on CPU usage, disk space usage, page views on a Web server, and almost any other data points available on the local network.

Cacti collects baseline (typical) data over time. You can use that information to gain insight into the ongoing behavior of a system and network, and to help resolve problems. The information can even predict what might happen in the future (e.g., when a disk is likely to become full).

Cacti periodically polls devices on a network for the data it needs, and stores the data in RRD files for use with RRDtool (round-robin database tool; oss.oetiker.ch/rrdtool). The Cacti Web interface allows you to browse a list of devices and graphs and see visual representations of device activity over time.

Cacti builds on the lessons learned from tools such as MRTG (oss.oetiker.ch/mrtg; page 975) and Cricket (sourceforge.net/projects/cricket). Each of these tools has the following characteristics:

- Periodically polls tracked devices for data. The tool most commonly used to collect this data is SNMP (Simple Network Management Protocol; www.net-snmp.org).
- Stores the data in an RRD file.
- Has a Web interface that allows you to examine graphs generated from the stored data. These graphs typically display daily, weekly, monthly, and yearly information.

Cacti’s configuration is performed through its Web interface, whereas MRTG and Cricket are configured by editing text files.

RRD files and RRDtool are the key to much of Cacti’s functionality. The Cacti Web site describes Cacti as “the complete RRDtool-based graphing solution.” RRD files store time-series data efficiently and, through the use of aggregation functions, make it easy to keep a lot of detail for recent time periods but progressively less detail as the data in the files ages. RRDtool easily generates both simple and complex graphs from RRD files.

### Extending Cacti

Many extensions and plugins are available for Cacti. Once you are familiar with the basic use and operation of Cacti, visit cacti.net/additional_scripts.php for a partial list of these additons. Also visit the documentation and the user forums at the same site to obtain more information about Cacti and to learn how you can add functionality and support for different devices and data sources.

## CONFIGURING SNMP

To monitor data sources on a system, you must install and run the SNMP daemon on that system as explained under “Setting Up a Data Source” on page 652. Displaying the automatically generated default graphs based on the local system is a good way to check that Cacti is working. To do so you must install and run the SNMP daemon on the local system. However, see the tip on page 647.

## SETTING UP LAMP

Cacti is a LAMP (Linux, Apache, MariaDB/MySQL, PHP) application; you must install and configure these applications before you can configure Cacti. This section explains how to set up the software on the system running Cacti.

### NOTES

See page 1114 for an explanation of why MySQL is now MariaDB.

When you set up LAMP, you use the MariaDB/MySQL databases named mysql and cacti. Fedora/RHEL sets up the mysql database when you install the MySQL/MariaDB server. You set up and populate the cacti database as explained under “Configuring MariaDB” on the next page.

The following database users must be set up. Each of these accounts should have a password:

- A user named root for the database named mysql. This user must be named root. The MariaDB installation script sets up this user.
- A user named cactiuser for the database named mysql. You can change this username, but as installed, Cacti is set up to use cactiuser.
- A Cacti administrative user for the database named cacti. As set up when you install Cacti, this user has the name admin and the password admin. You can set up additional Cacti user accounts.

As of this writing, Fedora/RHEL has Cacti 0.8.8a-8 in its repositories. Do not be misled by the pre-1.0 version number: Cacti is stable and in use on many systems.

### PREREQUISITES

Install the following packages:

- cacti
- mariadb (page 1118)
- mariadb-server (page 1118)
- php (installed with cacti)
- httpd (Apache; page 931; installed with cacti)
- rrdtool (installed with cacti)
- net-snmp (optional; needed only to monitor the local system)
- net-snmp-utils (optional)

If you want to work with Cacti from a browser on a system other than the one running Cacti, and the system running Cacti is running a firewall or is behind a firewall, you need to open TCP port 80 on the system running Cacti. Give the following commands to open the port each time the system boots (permanently) and on the running system; see page 906 for information on firewall-cmd.

```bash
# firewall-cmd --add-port=80/tcp
# firewall-cmd --permanent --add-port=80/tcp
```

When SELinux is set to use a targeted policy, httpd on the system running Cacti is protected by SELinux. For more information refer to “Setting the Targeted Policy with system-config-selinux” on page 475.

## CONFIGURING MARIADB

Install MariaDB and run systemctl to enable and start the mysqld daemon as explained under “Installing a MariaDB Server and Client” on page 1118. Be sure to assign a password to the MariaDB user named root by using either mysqladmin or mysql_secure_installation. For more help, see “Setting Up MariaDB” on page 1119.

> **Cacti does not create the default graphs automatically**
> A good way to make sure Cacti is working is by the presence of the automatically generated default graphs that are based on the device named localhost (the loopback network device). As of version 0.8.8a-8, a change in one of the Cacti installation files causes Cacti not to populate these graphs nor any graphs based on localhost. For a description of the change see the Web Page at svn.cacti.net/viewvc/cacti/branches/0.8.8/install/index.php?r1=6952&r2=6953.

Make the following change before the first time you start Cacti if you want Cacti to populate the automatically generated default graphs and any graphs you create based on localhost. This change is not necessary if you are interested only in graphs based on devices you set up, including devices on the local system. For more information on setting up a device that Cacti will monitor, see “Adding a Device” on page 653.

The change involves adding a line to the file named /usr/share/cacti/install/index.php. As of Cacti version 0.8.8a-8, line 358 of this file is as follows (do not change this line):

```sql
db_execute("delete from version");
```

Add the following line just above the preceding one (both lines are indented using one TAB character):

```php
repopulate_poller_cache();
```

Save the file and exit from the editor; continue with the installation and setup.

### Create the cacti database

Next, issue the following commands to create a database named cacti, create a mysql database user named cactiuser, grant that user the necessary privileges, and assign a password to that user. Replace cactipassword in the following example with your choice of a password. Although the FLUSH PRIVILEGES statement is not required, it is good practice to include it.

```bash
# mysql -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 11
...
MariaDB [(none)]> CREATE DATABASE cacti;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> GRANT ALL ON cacti.*
       -> TO cactiuser@localhost
       -> IDENTIFIED BY 'cactipassword';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> EXIT
Bye
```

### Set up and populate the cacti database

Give the following command to set up and populate the database named cacti. When MariaDB prompts for a password, provide the password for the MariaDB user named root (not the MariaDB user named cactiuser).

```bash
# mysql -p cacti < /usr/share/doc/cacti/cacti.sql
Enter password:
```

### Edit db.php

Most of the information in the /etc/cacti/db.php file is correct as installed. Edit this file to change the value assigned to $database_password from cactiuser to the same value you used for cactipassword when you created the cacti database (the password for the MariaDB user named cactiuser). Do not change the value assigned to $database_username.

```php
$database_type = "mysql";
$database_default = "cacti";
$database_hostname = "localhost";
$database_username = "cactiuser";
$database_password = "cactiuser";
$database_port = "3306";
$database_ssl = false;
```

## Configuring Apache

Apache is installed when you install Cacti. Modify the httpd.conf file as explained on page 936; if you do not make this modification, Apache will display errors when it starts but will work anyway. Use systemctl to enable and start the httpd daemon (page 935). Cacti supplies the content.

### Set the time zone

The /etc/php.ini file initializes many things including the time zone for Cacti. As installed, this file includes a commented-out example of how to set the time zone

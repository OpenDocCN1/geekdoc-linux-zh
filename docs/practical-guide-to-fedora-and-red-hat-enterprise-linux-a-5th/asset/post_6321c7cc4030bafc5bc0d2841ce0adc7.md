
Cacti is part of the next generation of monitoring tools. It builds on the lessons learned from tools such as MRTG (oss.oetiker.ch/mrtg; page 882) and Cricket (sourceforge.net/projects/criclet). Each of these tools:

- Periodically polls tracked devices for data. The method most commonly used to collect this data is via SNMP (Simple Network Management Protocol; www.net-snmp.org).
- Stores the data in an RRD file.
- Has a Web interface that allows you to examine graphs generated from the stored data. These graphs typically display daily, weekly, monthly, and yearly information.

Cacti’s configuration is performed through its Web interface, whereas MRTG and Cricket are configured by editing text files.

RRD files and RRDtool are the key to much of Cacti’s functionality. The Cacti Web site describes Cacti as “the complete RRDtool-based graphing solution.” RRD files store time-series data efficiently, and through the use of aggregation functions make it easy to keep a lot of detail for recent time periods but progressively less detail as the data in the files ages. RRDtool easily generates both simple and complex graphs from RRD files.

Extending Cacti

Many extensions and plugins are available for Cacti. Once you are familiar with the basic use and operation of Cacti, visit cacti.net/additional_scripts.php for a partial list. Also visit the documentation and the user forums for more information about Cacti and how you can add functionality and support for different devices and data sources.

## CONFIGURING SNMP

If you want to monitor data sources on the local system, install and run SNMP on the local system as explained under “Setting Up a Remote Data Source” on page 614.

## SETTING UP LAMP

Cacti is a LAMP (Linux, Apache, MySQL, PHP) application; you must install and configure these applications before you can configure Cacti. This section explains how to set up the software on the system running Cacti. See “Setting Up a Remote Data Source” on page 614 for an explanation of how to set up a system that Cacti will query and report on. By default, Cacti sets up the local system to run Cacti *and* be a data source.

**NOTES**
When you set up LAMP, you set up three accounts: two MySQL accounts and one Cacti account. Each of these accounts should have a password:

- A MySQL account for user named **root**. This account must be named **root**.
- A MySQL account for user named **cactiuser**. You can change this username, but as installed, Cacti is set up to use **cactiuser**.
- A Cacti administrative account for user named **admin** (initially the password is **admin**). You can set up additional Cacti user accounts.

As of this writing, the latest stable version of Cacti is 0.8.7e. Do not be misled by the pre-1.0 version number: Cacti is stable and in use on many systems.

## PREREQUISITES

Install the following packages (yum will also install many dependencies):

- cacti
- mysql (page 584)
- mysql-server (page 584)
- php
- httpd (Apache; page 841)
- net-snmp (optional; needed only to monitor the local system)
- net-snmp-utils (optional; includes snmpwalk)

The **snmpd** daemon, which runs on systems monitored by Cacti, uses UDP port 161. If the monitored system is running a firewall, you need to open this port (page 825). If you want to work with Cacti from a browser on a system other than the one running Cacti, you need to open TCP port 80 on the system running Cacti. For more information refer to “Firewall” on page 844. For more general information, see Chapter 25, which details the **iptables** utility.

When SELinux is set to use a targeted policy, both **httpd** (on the system running Cacti) and **snmpd** (on the systems being monitored) are protected by SELinux. You can disable this protection if necessary. For more information refer to “Setting the Targeted Policy with **system-config-selinux**” on page 416.

## CONFIGURING MYSQL

Install and start MySQL as explained starting at “Prerequisites” on page 585. Be sure to assign a password to the MySQL user named **root** by using either **mysql_secure_installation** or **mysqladmin**.

Next, use the following commands to create a database named **cacti**, create a MySQL user named **cactiuser**, grant that user the necessary privileges, and assign a password to that user. Replace *cacti_password* in the following example with your choice of a password. Although the FLUSH PRIVILEGES statement is not required, it is good practice to include it.

```
# mysql -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.1.39 Source distribution
Type 'help'; or '\h' for help. Type '\c' to clear the current input statement.
mysql> CREATE DATABASE cacti;
Query OK, 1 row affected (0.00 sec)
mysql> GRANT ALL ON cacti.*
-> TO cactiuser@localhost
-> IDENTIFIED BY 'cactipassword';
Query OK, 0 rows affected (0.00 sec)
mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
mysql> exit
Bye
```

Give the following command to set up and populate the database named **cacti**. When MySQL prompts for a password, provide the password for the MySQL user named **root** (not the MySQL user named **cacti**).

```
# mysql -p cacti < /usr/share/doc/cacti/cacti.sql
Enter password:
```

Most of the information in the `/etc/cacti/db.php` file is correct as installed. Edit this file to change the value assigned to **$database_password** from cactiuser to the same value as **cacti/password** in the preceding step (the password for the MySQL user named **cacti**). Do not change the value assigned to **$database_username**.

```
$database_type = "mysql";
$database_default = "cacti";
$database_hostname = "localhost";
$database_username = "cactiuser";
$database_password = "cactiuser";
$database_port = "3306";
```

## CONFIGURING APACHE

Install Apache as explained under “About Apache” on page 842. Modify the **httpd.conf** file as explained on page 845; if you do not make this modification, Apache will display errors when it starts but will work anyway. Run **chkconfig** and start the **httpd** daemon. Cacti supplies the content:

The `/etc/httpd/conf.d/cacti.conf` file controls the location and accessibility of Cacti on the Apache server. By default, Cacti is available as **127.0.0.1/cacti** (based on the Alias statement) and only a user on **127.0.0.1** (and not **localhost**: based on the Allow from statement) can access Cacti. The default **cacti.conf** file follows:

```
$ cat /etc/httpd/conf.d/cacti.conf
#
# Cacti: An rrd based graphing tool
# Alias /cacti /usr/share/cacti
<Directory /usr/share/cacti/>
    Order Deny,Allow
    Deny from all
    Allow from 127.0.0.1
</Directory>
```

To follow the example in this section, add an **Allow from localhost** line immediately below the **Allow from 127.0.0.1** line. You can add additional lines to allow access from other systems. The following `<Directory>` container allows access from 127.0.0.1, localhost, and the remote system at 10.10.4.98:

```
<Directory /usr/share/cacti/>
    Order Deny,Allow
    Deny from all
    Allow from 127.0.0.1
    Allow from localhost
    Allow from 10.10.4.98
</Directory>
```

See “Alias” (page 862), “`<Directory>`” (page 855), and “Allow” (page 868) for more information.

## ENABLING THE CACTI POLLER

Enable the Cacti poller by removing the hash mark from the left end of the line in the /etc/cron.d/cacti file. The *\*/5 causes **cron** to execute the script every five minutes.

```
$ cat /etc/cron.d/cacti
*\*/5 * * * * cacti /usr/bin/php /usr/share/cacti/poller.php > /dev/null 2>&1
```

## CONFIGURING CACTI

After starting or restarting Apache, point a Web browser on the machine running Cacti at **localhost/cacti**; Apache redirects the browser to the Cacti installation page at localhost/cacti/install and displays the Cacti Installation Guide screen. Click **Next**.

Confirm the information on the Cacti Installation Guide screen (Figure 17-9) and click **Next**.

![](img/f28adb66a7398a382f0505e0ba74a872_651_0.png)

**Figure 17-9** The Cacti Installation Guide screen

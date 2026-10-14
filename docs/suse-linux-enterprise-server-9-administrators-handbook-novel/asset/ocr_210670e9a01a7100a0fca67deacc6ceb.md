Both Snort and MySQL are included in the original distribution media for your SLES server. If they were not included in the original install, you can add them to your system using the YaST software option. Newer versions of the software are available from their respective websites.

As mentioned earlier, configuring Snort requires making changes to `/etc/snort/snort.conf`. The version of this file supplied with the default install will suffice for the original install. You may, however, want to modify the `/etc/init.d/snort` start script as mentioned previously to monitor events beyond the local server.

Once snort has been configured and is logging alerts to `/var/log/snort/alert`, you can proceed with the configuration of MySQL. Similarly to Snort, installing the MySQL database does not enable the startup of the database when the machine starts. To enable this feature and the associated clean shutdown, you must use the YaST Runlevel Editor.

By default, MySQL does not set a local administrator password. To set a password to protect the database, use the following command:

```
Athena:~ # mysqladmin -u root password newpassword
```

The results of a Snort scan should be stored in a Snort-specific database. To create such a database within MySQL, sign into MySQL using the root account just defined and use commands similar to these:

```
use mysql;
create database snort;
use snort;
grant ALL on snort.* to snort@Athena.UniversalExport.ca
  identified by 'mspiggy';
grant ALL on snort.* to snort@localhost identified
  by 'mspiggy';
exit
```

These commands create an empty database for the Snort alerts. Before you can make Snort point to MySQL, you need to create the tables it is expecting. In the original installation of Snort, a script is provided to create all the required structures. The file containing the script is `/usr/share/doc/packages.snort/create_mysql`. Enter MySQL using the Snort account this time and execute the preceding script:

```
Athena:~ # mysql -u snort -p
Enter password:
Welcome to the MySQL monitor.
Commands end with ; or \g.
```
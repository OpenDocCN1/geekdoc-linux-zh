
11:09:13 AM      190.00
11:09:15 AM     1013.50
11:09:17 AM     1349.00
11:09:19 AM     2071.00
11:09:21 AM     2132.00
11:09:23 AM     1643.50
11:09:25 AM     2194.00
Average:        1399.83

[root@UDBLNX06 root]# sar -n DEV -s 11:09:25 -f sartest.bin|egrep "eth0|IFACE"
11:09:25 AM     IFACE       rxpck/s   txpck/s    rxbyt/s    txbyt/s
11:09:27 AM     eth0     1187.00   2459.00   1511133.00   3007010.50
11:09:29 AM     eth0     1218.00   2528.50   1558313.00   3078301.00
11:09:31 AM     eth0     1219.00   2534.00   1558488.00   3085869.00
11:09:33 AM     eth0     1209.00   2504.50   1541410.50   3051547.50
11:09:35 AM     eth0     1181.00   2502.50   1504659.50   3050603.50
Average:        eth0     1202.80   2505.70   1534800.80   3054666.30

As mentioned in 6.3.3, "Iostat" on page 250, the sar utility is contained in sysstat package; before using this command, you need to make sure sysstat package is installed in your system.

For details about using the sar command, refer to the man help pages for sar or other Linux documentation.

## 6.3.5 Other system monitoring tools

There are also a multitude of Linux system monitoring tools available for monitoring Linux system resource usage, such as the ps command which is known to almost everybody is used to report processes status, pstree can be used to display a tree of processes, netstat for printing network related information, nfsstat for NFS specific statistics, and so forth. In addition, pgrep and pkill commands are very helpful when you want to look up or signal processes based on name and other attributes of processes. And if you like monitoring tools with graphical user interface, utilities like gnome-system-monitor and ksysguard also can be used. For more information, refer to Linux specific documentation.

## DB2 integrated tools and wizards

This chapter discusses some DB2 integrated tools available for the Linux platform for administration and development purposes. DB2 UDB provides a multitude of tools that make it much easier and more efficient to install and administer your database system, to continuously manage increasing volumes of data, to handle the tremendous growth in the number of users, to deliver better performance and to support different kinds of applications, and so forth.

Besides GUI tools, DB2 also provides many command line tools to assist you in administering the database system, such as you can use the DB2 Command Line Processor to execute DB2 administration commands and SQL statements, use db2mtrk to track DB2 memory usage by instance and database, as well as db2 agents, and use db2look to extract the needed DDL statements to reproduce the database objects.

Some tools and wizards have been discussed in other chapters of this book, as shown in Table 7-1 on page 256. For information regarding these tools and wizards, refer to those chapters.

## Table 7-1 Tools and wizards covered in other chapters

| Tool/Wizard | Usage | Chapter Number |
|---|---|---|
| db2setup | DB2 installation and instance creation | 2 |
| db2_install | DB2 package installation | 2 |
| Configuration Advisor | DB2 instance and database parameter configuration | 3 |
| Command Center | GUI tool for db2 commands and SQL statements execution | 3 |
| License center | Manage db2 licenses information | 3 |
| Backup/Restore | Database backup and recovery | 5 |
| Reorg | Reorganize table and indexes | 5 |
| Runstats | Statistics information collection | 5 |
| Export/Import | Table data export and import | 5 |
| Load | Load data into database | 5 |
| Task Center | Task setup and scheduling | 5 |
| Health Center | System health monitor configuration | 6 |
| Development Center | Integrated tool for stored procedure, UDF development | 8 |

In this chapter, we select a few tools and wizards to discuss in detail. For the entire DB2 UDB tools and wizards collection, refer to IBM DB2 UDB Guide to GUI Tools for Administration and Development, SC09-4851. That book focuses on introducing GUI tools, and many tools are covered. In addition, you can also read IBM DB2 UDB Command Reference V8, SC09-4828, to acquire more information about tools and utilities provided by system and DB2 CLP commands.

In general, to invoke GUI tools in DB2 UDB for the Linux platform, you can start them from DB2 Control Center. To start DB2 Control Center, click the Control Center icon available on the Linux desktop, or enter the command "db2cc" from the command line, and then press enter. Most GUI tools can be invoked from the Control Center, as Figure 7-1 shows; there is a tools menu available for you to choose the desired tool. In addition, another pop-up window which contains choices of wizards will show up if you clicked the "Wizards..." item within tools

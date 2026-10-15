> **Note:** We chose the number 99 because the number between letter S and the name should be greater than the number on all other links in the rc5.d directory for this script to be executed last.

Like Red Hat, you can change kernel parameters at run-time (for testing purposes) using the sysctl -w command. For example, to change the semaphore array parameter, enter:

```
sysctl -w kernel.sem="250 32000 32 1024"
```

Remember, these settings will only be saved at the next reboot if they are in the /etc/sysctl.conf file.

# 2.1.6 Additional software requirements

Depending on your DB2 requirements, you may be required to install additional software packages for DB2 to function properly. Make sure that the following software is installed prior to using DB2.

+   - The IBM Java Developer's Kit (JDK) Version 1.3.1, Service Release 1, This is required to run DB2 graphical tools, and to create and run Java applications, including stored procedures and user-defined functions. If the correct version of JDK is not already installed, it will be installed for you during the installation process if you use DB2 Setup or a response file. The db2_install utility does not install the JDK for you. Refer to the end of this section for instructions about how to install the JDK...

> **Note:** If you have another version of the JDK installed on your machine, we recommend that you remove it before installing DB2. The Control Center may not launch if two different versions of the JDK co-exist on your machine. If your application requires the existing JDK or JRE, you may be required to disable it by unsetting environment information such as PATH or CLASSPATH before installation.

+   - Web browser, to view DB2 HTML documentation.

+   - X Window System software, capable of rendering a graphical user interface. You need this if you want to use the DB2 Setup wizard to install DB2 (it's a graphical installer) or any DB2 graphical tools.

+   - Additional software, provided in the following tables (Table 2-4 and Table 2-5). The pdksh package is required for all DB2 systems, and the rsh-server and nfs-utils packages are mostly required for partitioned database systems.
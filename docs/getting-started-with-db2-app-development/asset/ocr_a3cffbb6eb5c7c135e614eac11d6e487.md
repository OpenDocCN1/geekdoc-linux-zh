+   3. On Linux, ensure you have the gcc compiler and the following development packages: apache-devel, autoconf, automake, bison, flex, gcc, and libxml2-devel package

+   4. If the Web server where the PHP code is and the database server are on different machines, download and install one of the following DB2 clients: IBM Data Server Driver Package, IBM Data Server Client, or IBM Data Server Driver for ODBC and CLI. These can be found at this location: http://www-01.ibm.com/support/docview.wss?rs=4020&uid=swg21385217

+   5. Download the latest version of the PHP from http://www.php.net for Linux/UNIX or Windows. The latest version of PHP at the time of writing is PHP 5.3. Install it, and configure it. The following sections explain how to do this on Linux/UNIX and Windows.

# 8.2.1.1 Setting up the PHP environment manually on Linux or UNIX

+   1. Untar the PHP package previously downloaded by issuing the following command: tar -xjnf php-5.x.x.tar.bz2

+   2. Change directories into the newly created php-5.x.x directory.

+   3. Configure the makefile by issuing the configure command. Specify the features and extensions you want to include in your custom version of PHP. A typical configure command includes the following options:

```
./configure --enable-cli --disable-cgi --with-
 apxs2=/usr/sbin/apxs2 --with-zlib --with-pdo-ibm=<sqllib>
Where --with-pdo-ibm=<sqllib> enables the pdo_ibm driver using the DB2
CLI library to access DB2 databases. The <sqllib> setting refers to the directory
where DB2 was installed. The pdo_ibm driver is discussed in more detail later in
this chapter.
```

+   4. Compile the files by issuing the make command.

+   5. Install the files by issuing the make install command. Depending on how you
+    configured the PHP install directory using the configure command, you may
+   need root authority to successfully issue this command. This should install the
+    executable files and update the Apache HTTP Server configuration to support
+   PHP.

+   6. Install the ibm_db2 extension by issuing the following command as a user with
+    root authority: pecl install ibm_db2
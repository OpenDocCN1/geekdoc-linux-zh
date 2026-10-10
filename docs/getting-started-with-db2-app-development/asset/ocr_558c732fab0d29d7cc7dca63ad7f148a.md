8. C. IBM_DB adapter utilizes the IBM Driver for **ODBC** and **CLI** to connect to IBM data servers.

9. A. The **Account** is optional.

10. B.

# ## Chapter 8

+   1. As the name suggests, the non persistent connection disconnects and frees up the connection resources after each db2_close, or connection resource is set to NULL, or the script ends.
+   
+   In the case of persistent connections, the connection resources are not freed up after a db2_close or the script is exited. Whenever a new connection is requested, PHP tries to reuse the connection with the same credentials

2. Connection pooling helps database application performance due to the reduction of new connections by reusing the old connections established before. It can be beneficial when the connections made have a short duration.

3. Enable PHP support in Apache HTTP Server 2.x by adding the following lines to the `httpd.conf` file, where `phplibdir` refers to the PHP install directory:

```
```
    LoadModule php5_module 'phplibdir/php5apache2.dll'
    AddType application/x-httpd-php .php
    PHPIniDir 'phplibdir'
```
```

4. To determine the configuration file path issue the `php -i` command and look for the `php.ini` keyword

5. The *ibm_db2* extension API makes porting an application that was previously written for Unified ODBC almost as easy as globally changing the "odbc_" function name to "db2_" throughout the source code of your application.

+   - D
+   - B
+   - D
+   - C
+   - A

# ## Chapter 9

1. Perl Database Interface (DBI)
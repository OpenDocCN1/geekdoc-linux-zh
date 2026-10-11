# 12

# General MySQL Administration

This chapter discusses the responsibilities that you must carry out to keep MySQL running smoothly if you administer MySQL at your site:

+   * Securing your MySQL setup after installing it
+   * Making sure that the server is up and running as much of the time as possible
+   * Setting up user accounts so that clients can access the server
+   * Maintaining server logs
+   * Modifying and monitoring the server's operating parameters for better performance
+   * Running multiple servers
+   * Determining whether and when to upgrade MySQL to a newer version

Other significant administrative concerns are covered in Chapter 13, “Access Control and Security,” and Chapter 14, “Database Maintenance, Backups, and Replication.”

This chapter covers several programs that are essential for MySQL administrators to know about:

+   * *mysqld* is the MySQL server.
+   * *mysqld_safe*, *mysql_server*, and *mysql_multi* are used for starting the server.
+   * *mysqladmin* performs miscellaneous administrative operations.

Much of the information in this chapter can be better appreciated if you have an understanding of MySQL's data directory, which is where the server stores databases, log files, and other information. For details, see Chapter 11, “The MySQL Data Directory.” For additional information specific to the SQL statements and programs discussed here, see Appendix E, “SQL Syntax Reference,” and Appendix F, “MySQL Program Reference.”

Note
For simplicity (and to keep pathnames shorter), most of the Windows-related material in this chapter assumes that MySQL is installed at *c:*\*mysql*. However, the MySQL installation wizard for Windows likes to install the distribution under *C:*\*Program Files*\*MySQL*\*MySQL*
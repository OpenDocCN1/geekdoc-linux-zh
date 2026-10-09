# History

MySQL (My Structured Query Language) is an implementation of SQL. It is the world’s most popular open-source RDBMS (relational database management system). It is extremely fast and is used by some of the most frequently visited Web sites on the Internet, including Google, Facebook, Twitter, Yahoo, YouTube, and Wikipedia. Recently, however, some of these companies have moved to MariaDB, which is explained next. Fedora/RHEL has replaced MySQL in its repositories with MariaDB, and Wikipedia has also converted.

Michael “Monty” Widenius and David Axmark started development of MySQL in 1994. In 2008 Sun Microsystems bought MySQL.

In 2009, not happy with the development process of MySQL under Sun Microsystems, Mr. Widenius left Sun and founded a company named The Monty Program to work on a fork of MySQL named MariaDB. In 2010, when Oracle Corporation acquired Sun Microsystems, most of the MySQL developers left Sun to join the MySQL forks MariaDB and Drizzle (www.drizzle.org).

Today, MariaDB is a community-developed fork of MySQL that is dedicated to FOSS software (page 7) released under the GNU GPL (page 5). Currently, MariaDB is a drop-in replacement for MySQL and uses the same commands as MySQL; only the package names differ (but see mariadb.com/kb/en/mariadb-vs-mysql-compatibility). However, MariaDB is planning to introduce significant changes in the next version; at that time there might no longer be compatibility at the feature level. However, one would expect MariaDB to maintain protocol compatibility with MySQL into the future. Visit mariadb.com/blog/explanation-mariadb-100 for more information.

# MariaDB or MySQL?

> Because MariaDB is a fork of MySQL, almost all of the code is the same. The places where the code differs do not affect the examples or descriptions in this chapter. The examples in this chapter were tested against MariaDB. If you want to work with MySQL, install the community-mysql package. Unless you explicitly install the community-mysql package, Fedora installs MariaDB. For more information visit fedoraproject.org/wiki/Features/ReplaceMySQLwithMariaDB.

Many programming languages provide interfaces and bindings to MariaDB, including C, Python, PHP and Perl. In addition, you can access a MariaDB database using the industry-standard ODBC (Open Database Connectivity) API. You can also call MariaDB from a shell script or the command line. MariaDB is a core component of the popular LAMP (Linux, Apache, MariaDB, PHP/Perl/Python) open-source enterprise software stack.

# NOTES

MariaDB has a separate set of users from Linux: Users who have MariaDB accounts might not have Linux accounts, and vice versa. As installed, the name of the MariaDB administrator is root. Because the MariaDB root user is not the same as the Linux root user, it can (and should) have a different password.
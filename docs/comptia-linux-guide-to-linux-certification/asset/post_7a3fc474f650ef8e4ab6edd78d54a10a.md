
### E-mail Services

E-mail servers typically accept e-mail and route it over the Internet using Simple Mail Transfer Protocol (SMTP) or Enhanced Simple Mail Transfer Protocol (ESMTP) on TCP port 25. Additionally, client computers can retrieve e-mail from e-mail servers using a variety of different protocols such as Post Office Protocol (POP) or Internet Message Access Protocol (IMAP). Client computers can also send e-mail to e-mail servers using SMTP/ESMTP for later relay on the Internet.

Most e-mail servers provide the functions of the Mail Transfer Agent (MTA) and Mail Delivery Agent (MDA) described earlier in Chapter 1.

To relay e-mail to other servers on the Internet, an e-mail server must look up the name of the target e-mail server in the domain’s MX (Mail Exchanger) records, which are stored on a public DNS server. For example, if your local e-mail server needs to send e-mail to jason.eckert@trios.com, the e-mail server locates the name of the target e-mail server by looking up the MX record for the trios.com domain. It then resolves the target e-mail server name to the appropriate IP address using the A (host) record for the server on the public DNS server.

Daemons and other system components on Linux systems rely on e-mail to send important information to the root user. The most common e-mail daemon used in modern Linux systems is Postfix.

> Fedora 20 is one of the few Linux distributions that does not install an e-mail daemon by default.

The Postfix daemon is configured by default to accept e-mail on TCP port 25 and route it to the appropriate user on the Linux system. To test this, you can use the `telnet` command with port 25 as an argument. This displays a Welcome banner that identifies the e-mail server, as shown in the following output. Additionally, you can use the `EHLO` command to test ESMTP support and the `HELO` command to test SMTP support, as shown in the following output:

```bash
[root@server1 ~]# telnet localhost 25
Connected to localhost.
Escape character is '^]' .
220 server1.class.com ESMTP Postfix
EHLO sample.com
250-server1.class.com
250-PIPELINING
250-SIZE 10240000
250-8BITMIME
250-ETRN
250-ENHANCEDSTATUSCODES
250 DSN
HELO sample.com
250 server1.class.com
quit
221 2.0.0 Bye
Connection closed by foreign host.
[root@server1 ~]#
```

To check your e-mail on your local Linux system, you can use the `mail` command, as shown here:

```bash
[root@server1 ~]# mail
Mail version 8.1.2 01/15/2001. Type ? for help.
/var/spool/mail/root": 13 messages 6 new 10 unread
U 1 Cron Daemon Sat Jul 11 07:01 26/981 "Cron"
U 2 logwatch@localhost.1 Mon Jul 20 11:43 42/1528 "Logwatch"
U 3 logwatch@localhost.1 Tue Jul 21 12:32 151/4669
N 4 jason.eckert@trios.com Wed Sep 29 15:53 11/430
& 4
Message 4:
From jason.eckert@trios.com Wed Sep 29 15:53:25 2009
Return-Path: <jason.eckert@trios.com>
Date: Wed, 29 Sep 2010 15:52:36 -0400
From: jason.eckert@trios.com
Status: R

Hey dude

& q
[root@server1 ~]#
```

The `mail` command is an example of a Mail User Agent (MUA), as described in Chapter 1. E-mail for each user is stored within a file named for the user in the /var/spool/mail directory. For example, the e-mail for the bob user will be stored within the /var/spool/mail/bob file. The /etc/aliases file contains other e-mail names that are used to identify the different users on the system. From the entries in the /etc/aliases file shown next, you can use the names postmaster, bin, daemon, or adm to refer to the root user:

```bash
[root@server1 ~]# head -17 /etc/aliases
# See man 5 aliases for format
postmaster: root
bin:		root
daemon:		root
adm:		root
[root@server1 ~]#
```

If you modify the /etc/aliases file, you need to run the `newaliases` command in order to rebuild the aliases database (/etc/aliases.db) based on the entries in the /etc/aliases file. Only the aliases database is used by the Postfix daemon.

Users can also create a .forward file in their home directory that lists the user name or email address that mail items should be forwarded to.

While Postfix is normally configured to accept and route local e-mail only, you can also configure it to relay e-mail to other servers on the Internet as well as accept connections from e-mail clients on your network using POP and IMAP. To do this, you must edit its configuration file: /etc/postfix/main.cf. A common set of lines that you should modify or add at minimum is listed in Table 13-4.

| Line | Change |
| :--- | :--- |
| mydomain = sample.com | Sets the e-mail domain name; changes to desired name |
| myorigin = $mydomain | Sets local access to the domain name |
| inet_interfaces = all | Configures Postfix to listen for e-mail on all interfaces |
| mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain | Configures destination domain for e-mail |
| mynetworks_style = class | Trusts e-mail from computers on the local network |

**Table 13-4** Sample lines in /etc/postfix/main.cf to modify or add when configuring Postfix

### Database Services

Databases are large files that store important information in the form of tables. A table organizes information into a list. Within the list, the set of information about a particular item is called a record. For example, in a list of customer mailing addresses, a single record would contain a customer's first name, last name, street address, city, state, and Zip code. The various categories of information within a record are called fields. For example, in our customer mailing address example, one field contains the city information, one contains the state information, and so on.

Most databases consist of dozens or hundreds of tables that store information used by applications. For example, accounting software typically stores financial data within a database. In large databases, information within certain tables can be related to information within other tables in the same database. These databases are called relational databases, and the tables within are usually linked by a common field. Figure 13-8 shows a simple relational database that consists of two tables with a related EmployeeID field.

Structured Query Language (SQL) is a special programming language used to store and access the data in databases. The database server programs that allow users to access and update the data stored within a database are called SQL servers. Table 13-5 lists common SQL statements that are used to manipulate data on SQL servers.

**Figure 13-8** A simple relational database structure

| Command | Description |
| --- | --- |
| CREATE DATABASE database_name | Creates a database |
| DROP DATABASE database_name | Deletes a database |
| CREATE TABLE table_name field_definitions | Creates a table within a database |
| DROP TABLE table_name | Deletes a table within a database |
| INSERT INTO table_name VALUES record | Inserts a new record within a table |
| UPDATE table_name SET record_modifications | Modifies records within a table |
| DELETE FROM table_name record | Deletes a record within a table |
| SELECT * FROM table_name | Displays all records within a table |
| SELECT fields FROM table_name WHERE criteria | Displays one or more fields for records within a table that meet a specific criteria |
| SELECT fields FROM table_name GROUP BY field | Displays one or more fields for records within a table and groups the results according to the values within a common field |
| SELECT fields FROM table_name ORDER BY field [ASC/DESC] | Displays one or more fields for records within a table and sorts the results in ascending or descending order according to the values within a common field |
| SELECT fields FROM table1 INNER JOIN table2 ON table1.common_field = table2.common_field | Displays one or more fields for records within two related tables (table1 and table2) that have a common field; only records that have matching information within the common field in both tables are displayed |
| SELECT fields FROM table1 LEFT OUTER JOIN table2 ON table1.name.common_field = table2.name.common_field | Displays one or more fields for all records within table1 and any records within table2 that have matching information within a common field |
| SELECT fields FROM table1 RIGHT OUTER JOIN table2 ON table1.name.common_field = table2.name.common_field | Displays one or more fields for all records within table2 and any records within table1 that have matching information within a common field |
| CREATE USER user_name WITH PASSWORD password | Creates a user that can access the SQL server |
| GRANT permissions ON table1 TO user_name | Assigns permissions to a user that give the user the ability to work with the table, where permissions can include INSERT, UPDATE, SELECT, or DELETE |

**Table 13-5** Common SQL statements

SQL servers usually offer advanced backup, repair, replication, and recovery utilities for the data within the database. In addition, SQL servers can store multiple databases, and they allow programs to access these databases from across the network. Thus, a single SQL server can store the data needed by all programs that exist on servers and client computers within the network. Although there are several SQL servers available for Linux, PostgreSQL is one of the most widely used.

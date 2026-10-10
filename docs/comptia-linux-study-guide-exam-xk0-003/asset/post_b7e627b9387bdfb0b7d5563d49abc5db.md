
require no password for administrative access. To enable a password, type the following command:

```
$ mysqladmin -u root password newpassword
```

Change newpassword to the password you want to use, of course. If your system already has a root password set, you can change it with another command:

```
$ mysqladmin -u root -p'oldpassword' password newpassword
```

Some distributions, such as Ubuntu, include installation scripts that prompt you to enter a MySQL root password when you install the software. Thus, you might not need to type these commands.

Typically, MySQL is started and stopped using SysV startup scripts, such as /etc/init.d/mysqld. Chapter 4 describes SysV startup scripts in more detail, so consult it if you need help starting or stopping MySQL. You can verify that MySQL is running using ps; search for a process called mysqld:

```
# ps ax | grep mysql
1948 ? S 0:00 /bin/sh /usr/sbin/mysqld_safe
2013 ? S1 33:30 /usr/sbin/mysqld --basedir=/usr\
--datadir=/var/lib/mysql --user=mysql --pid-file=/var/run/mysql/mysqld.pid
--skip-locking --port=3306 --socket=/var/run/mysql/mysql.sock
2014 ? S 0:00 logger -p daemon.err -t mysqld_safe -i -t mysql
30933 pts/0 S+ 0:00 grep mysql
```

In this example, the /usr/sbin/mysqld program is the MySQL server, so it's definitely running. This output also shows the options used to launch the program. Three other MySQL-related processes were also found by this query, including the grep command used to search for MySQL. Be sure that you find mysqld (the daemon, whose name ends in d); the mysql program is the client, and it could be running even if the server isn't running. If you can't find the MySQL daemon running, try using its SysV startup script, and if that fails, search your log files for clues to what might be going wrong when you try to launch the server.

## Testing the MySQL Connection

To test MySQL's basic operation, you should first ensure that the server is running, as just described. You can then start the SQL client. In the case of MySQL, this program is called mysql:

```
$ mysql
```

If the client can connect to a server, you'll see a mysql> prompt. If the server isn't running or can't be contacted, you'll see an error message. To verify the status of the mysql client connection to its server, you can use the STATUS command:

```
mysql> STATUS;
--------------------------
mysql Ver 14.12 Distrib 5.0.51a, for debian-linux-gnu (x86_64) using readline 5.2

Connection id:			29
```

Several additional lines of status information will appear, as well. You can peruse these to learn a few more details, such as what version of the server is in use and how long it has been running.

If you've just installed MySQL, it may have no databases defined. To learn what's defined, you can use the SHOW DATABASES command:

```
mysql> SHOW DATABASES;
+--------------------+
| Database			|
+--------------------+
| information_schema |
+--------------------+
1 row in set (0.00 sec)
```

These operations should be more than sufficient to verify basic functioning of MySQL. You might not get in so easily, though, particularly if you use a computer other than the one on which the MySQL server is running to test the server's operation. (If network operation is important in your installation, you should definitely test network access to ensure that firewalls or other network issues won't cause problems.) If you receive a Can't connect to MySQL server message, chances are either the MySQL server isn't running or a network configuration is blocking access to the server. If you receive an Access denied message, the problem is with authentication—you must specify a legal account and password.

To connect to a remote server, use a particular MySQL account, or send a particular MySQL password, you must use the --host (or -h), --user (or -u), or --password (or -p) options, respectively. For instance, to connect to the MySQL server running on third.luna.edu as dbuser with a password of e4bUg7TQ, you might type the following:

```
$ mysql --host=third.luna.edu -u dbuser -pe4bUg7TQ
```

![](img/9903a4d3f7abd8dcbef1035fa04a3406_542_0.png)

When using the long option names, you must include an equal sign between the option name and its value, as in the --host option in this example. An equal sign is not used with the short option forms. For the password, you must not include a space between the short option name (-p) and the password. You might prefer to use the long form (as in --password=e4bUg7TQ) to improve legibility. If you include the -p option but omit the password, mysql will prompt for it.

## Summary

Network servers are many and varied, and Linux provides programs to handle all common network protocols. These include DHCP for configuring clients' network settings, DNS for resolving hostnames and IP addresses, NTP for managing time on a network, SMB/CIFS for file sharing with Windows, NFS for file sharing with Linux and Unix, FTP for cross-platform file transfers, HTTP for Web browsing, VNC for cross-platform GUI access, SMTP for push e-mail, POP and IMAP for pull e-mail, and SQL for database access.

Although these servers share certain common features, such as their ability to be launched via SysV startup scripts or super servers, each protocol and server is unique. Indeed, for many protocols, multiple servers are available, and each server can have its own unique configuration style. Thus, you must study each server you install and run to determine how best to manage it.

## Exam Essentials

- Explain where Samba and NFS are best deployed. Samba is an implementation of the SMB/CIFS protocol suite, which is most often used for file and printer sharing by Windows systems; thus, Samba is best used as a server for Windows clients. NFS, by contrast, was designed as a file sharing protocol for Unix systems, so it's best used for sharing files with Unix or Linux clients.

- Describe the Samba and NFS configuration files. Samba is configured via smb.conf, which is typically stored in /etc/samba, or /etc/samba.d. Global Samba options appear in the [global] sections, and subsequent sections define specific shares. NFS is configured via /etc/exports, which lists the directories that are to be exported, one per line. Each line also contains a list of computers or networks that may mount the export, along with mount options.

**Summarize the differences between FTP and HTTP.** The File Transfer Protocol (FTP) is a login-based protocol for transferring files. The Hypertext Transfer Protocol (HTTP) doesn't typically require logins (although some Web sites do implement login functionality). FTP is an old protocol with some quirks, such as requiring the use of two network connections. The World Wide Web (WWW or Web for short) is built atop HTTP, making HTTP an extremely important protocol on today's Internet.

**Describe common Web server scripting tools.** The Common Gateway Interface (CGI) is a general mechanism that enables a Web server to run a normal Linux program or script (written in Perl, Python, C, or any other language that Linux supports) to generate Web pages dynamically. PHP and Tomcat are more specialized languages that are designed with Web use in mind. They require additional configuration in Samba but can be easier to program for Web purposes.

**Explain the purpose of rdesktop and VNC.** The `rdesktop` program enables access to Windows computers that provide the Windows-specific Remote Desktop Protocol (RDP) for remote login access. VNC can fill a similar role, but VNC is a cross-platform tool; the server can run Windows, Mac OS, Linux, or various other OSes.

**Describe the purpose of SQL and MySQL.** The Structured Query Language (SQL) is a common database language; it's used to store data that can be retrieved by individuals or programs. SQL is network-enabled, meaning that database users can exist on computers other than the one that hosts the database. MySQL is a common implementation of SQL for Linux; it includes client, server, and support programs.

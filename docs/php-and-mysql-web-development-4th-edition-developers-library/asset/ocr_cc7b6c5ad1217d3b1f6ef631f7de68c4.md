```
FIELDS ESCAPED BY '' LINES TERMINATED BY '';
SELECT * FROM tmp INTO OUTFILE 'x.MYI'
FIELDS ESCAPED BY '' LINES TERMINATED BY '';
```

+   3. After executing those statements, the test database directory also will contain files named x.frm, x.MYD, and x.MYI. In other words, the test database will contain a table x that is a stolen duplicate of the table in the other_db database.

To avoid having someone attack your users' tables in the same way, set the permissions on your data directory contents according to the instructions in given earlier in Section 13.1.2, "Securing Your MySQL Installation." As an additional measure, avoid granting the SHOW DATABASE privilege and run the server with the --skip-show-database option. This prevents users from using SHOW DATABASES and SHOW TABLES for databases to which they have no access, and helps to keep users from finding out about databases and tables they shouldn't be accessing.

The dangers of the FILE privilege are amplified if you run the MySQL server as root. That's inadvisable in the first place, and is particularly so when combined with the FILE privilege can do as well, even a user who has connected from a remote host. The server won't create a file that already exists, but it's sometimes possible to create new files that will alter the operation of the server host or compromise its security. For example, if any of the files /etc/resolv.conf, /etc/hosts, equiv, /etc/ssh/known_hosts, or /etc/sudoers do not already exist, a user who is able to cause the MySQL server to create them can drastically change the way your server host behaves. To avoid these problems, don't run mysqld as root. (See Section 12.2.1.1, "Running the Server Using an Unprivileged Login Account.")

The PROCESS and SUPER privileges should be granted only to trusted MySQL accounts. With PROCESS, a user can use SHOW PROCESSLIST to see the text of statements being executed by the server. This enables a user to snoop on other users and possibly see information that should remain private. With SUPER, the user can kill statements being executed by other users, disrupting their activities. SUPER also enables a user to purge log files and perform other actions that can compromise server operation.

Don't give the RELOAD privilege to people who don't need it. RELOAD enables a user to issue FLUSH and RESET statements, which can be abused in several ways:

+   - Binary and relay log files are created with names that form a numbered sequence. If you have configured the server to perform binary or relay logging, each FLUSH LOGS statement creates the next log in the sequence. A user with the RELOAD privilege who performs many log flushing operations can cause the server to create large numbers of files.
+   - A user with the RELOAD privilege can defeat the resource management mechanism by reloading the grant tables with FLUSH PRIVILEGES or with FLUSH USER_RESOURCES. Both statements reset resource management counters to zero.
Shellcodes: No Result
Papers: No Result

# Listing 904 - SearchSploit for MariaDB

Unfortunately, none of these would work for our version of MariaDB. Let’s broaden the scope and see what we get for MySQL.

```
kali@kali:~$ searchsploit mysql

Exploit Title										Path (\usr/share/exploitdb)/
-------------------------------------------------------
MySQL (Linux) - Database Privilege Escalation	exploits/linux/local/23077.pl
MySQL (Linux) - Heap Overrun (PoC)					exploits/linux/local/23076.pl
MySQL (Linux) - Stack Buffer Overrun (PoC)		exploits/linux/dos/23075.pl

MySQL 3.x/4.x - ALTER TABLE/RENAME Forces Old Permi	exploits/linux/remote/24669.txt
MySQL 4.0/17 (Linux) - User-Defined Function (U	exploits/linux/local/11181.c
MySQL 4.1.18/5.0 - Auth - Local/Remote Information Leak	exploits/linux/remote/1742.c
MySQL 4.1/5.0 - Authentication Bypass				exploits/multiple/remote/24250.pl
MySQL 4.1/5.0 - Zero-Length Password Authentication	exploits/multiple/remote/311.pl
MySQL 4.x - CREATE FUNCTION Arbitrary libc Code Exe	exploits/multiple/remote/25209.pl
MySQL 4.x - CREATE FUNCTION mysql.func Table Arbitr	exploits/multiple/remote/25210.php
MySQL 4.x - CREATE Temporary TABLE SymLink Priviled	exploits/multiple/remote/25211.c
MySQL 4.x/5.0 (Linux) - User-Defined Function (UDF)	exploits/linux/local/1518.c
MySQL 4.x/5.0 (Windows) - User-Defined Function Com	exploits/windows/remote/2374.txt
MySQL 4/5 - Server Date_Format Denial of Service	exploits/linux/dos/28234.txt
MySQL 4/5 - SUID Routime Miscalculation Arbitrary D	exploits/linux/remote/28398.txt
MySQL 4/5/6 - UDF For Command Execution					exploits/linux/local/7856.txt
MySQL 5 - Command Line Client HTML Special Character	exploits/linux/remote/32445.txt
MySQL 5.0.18 - Query Logging Bypass					exploits/linux/remote/27326.txt

MySQL Squid Access Report 2.1.4 - HTML Injection		exploits/php/webapps/20955.txt
MySQL Squid Access Report 2.1.4 - SQL Injection / C		exploits/php/webapps/44483.txt
MySQL User-Defined (Linux) (x32/x86_64) - 'sys'		exploits/linux/local/46249.py
MySQL yaSSL (Linux) - SSL Hello Message Buffer Over		exploits/linux/remote/16849.rb
MySQL yaSSL (Windows) - SSL Hello Message Buffer Ov	exploits/windows/remote/16701.rb

Paper Title										Path (\usr/share/exploitdb-papers)/
-------------------------------------------------------
MySQL Session Hijacking over RFI				docs/english/13708-mysql-session-hijacking-ove
MySQL UDF Exploitation				docs/english/44139-mysql-udf-exploitation.pdf
MySQL: Secure Web Apps - SQL Injection			papers/english/12945-mysql-secure-web-apps-s
Nobel contributions to the field - Ho			docs/english/40143-nobel-contributions-to-the-
...

```

# Listing 905 - SearchSploit for MySQL
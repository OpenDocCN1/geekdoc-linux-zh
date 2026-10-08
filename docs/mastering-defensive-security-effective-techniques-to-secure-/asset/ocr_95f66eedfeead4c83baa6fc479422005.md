422 Leveraging Pentesting for Defensive Security

The next step is to run the exploit, which is quite easy. First, you need to copy the path of the script with the following command:

```
searchsploit -p 34087
```

Then, as seen in the following figure, you will get a response with the full path of the script. Just copy and paste that path and you will be able to run the exploit!

```
kali@kali:~$ searchsploit -p 34087
Exploit: Joomla! Component Youtube Gallery 4.1.7 - SQL Injection
URL: https://www.exploit-db.com/exploits/34087
Path: /usr/share/exploitdb/exploits/php/34087.txt
File Type: ASCII text, with CRLF line terminators
```

Figure 15.20 - Obtaining the path to execute the exploit on Searchsplit

As mentioned before, executing those exploits is very easy, therefore it is one of the reasons why you need to make sure you test those vulnerabilities before they are exploited by an attacker.

# sqlmap

sqlmap is a very powerful penetration testing tool to detect and exploit SQL injection vulnerabilities on database servers. It is packed with a lot of cool features, including the following:

+   - Upload and download files.
- Dump entire database tables.
- Advanced search for specific tables or columns across databases.
- Enumeration of users, password hashes, roles, tables, columns, and more.
- Recognition of password hashes and support to crack them with dictionary-based attacks.

Additionally, sqlmap fully supports most common SQL servers, including MySQL, PostgreSQL, Microsoft SQL, Microsoft Access, and SQLite.

sqlmap is already preinstalled on Kali Linux, if you want to learn more about the tool, you can type the following command, which highlights the basic commands of the tool:

```
sqlmap -h
```
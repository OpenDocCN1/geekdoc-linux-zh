
Even if this sounds incredible, there are times when you may even find passwords in a .txt file, as illustrated in the following code example:

```
site:yoursite.com intitle:"index of" "Index of /" password.txt
```

The code shown in the preceding example will search for misplaced files (such as a .txt file with usernames or passwords).

> Tip
> Here, you can find more than 6,000 Google dorks that you can modify based on your needs. Some are specific to particular web services, so they may be really useful for you: https://www.exploit-db.com/google-hacking-database.

There is another way to prevent outsiders from using these Google dorks against your web systems by modifying the robots.txt file in your server, as follows:

- Prevent indexing from Google by running the following code:

User-agent: Googlebot
Disallow: /

- Prevent Google from indexing a specific file type by running the following code:

User-agent: Googlebot
Disallow: /*.sql$

- Prevent indexing of a given folder by running the following code:

User-agent: Googlebot
Disallow: /directoryName/

- Prevent indexing from other search engines by running the following code:

User-agent: *
Disallow: /

All these are very basic (but feasible) attacks, but now you have learned how to set up the basics of web security, it's time to move on to the next step and learn about the most common attacks on web applications.

# Leveraging DVWA

Before moving on with the rest of the chapter, you need to know this great tool that will help you to better understand the vulnerabilities on web applications.

But also, we are going to use this platform to show you how you can test your web application against the most common attacks, such as the following:

- Brute-force attacks
- SQL injection attacks

Additionally, this lightweight and easy-to-install system has a lot of cool features such as the:

- A platform to explore several web application vulnerabilities in a safe environment
- A great tool to create videos or real-time demos to raise awareness about those vulnerabilities
- A test environment to determine the impact of attacks on web applications
- A sandbox environment to test remediation actions

As mentioned, I strongly suggest you install the DVWA on a VM so that you can execute the labs that we will see in the upcoming section of this chapter, to see how to test your web applications against real attacks and the importance of applying at least basic security hardening in your web applications.

# Installing DVWA on Kali Linux

It is not easy to find clear (step-by-step) instructions to install DVWA on the latest version of Kali Linux; therefore to save you some time (and headaches), I created a super-easy-to-follow guide to help you install DVWA on Kali Linux in 14 steps. Here's how you do it:

- 1. Navigate to the html folder, as follows:

```
cd /var/www/html
```

- 2. Clone the git repository, like this:

```
sudo git clone https://github.com/digininja/DVWA.git
```

- 3. Change permissions over the installation folder, as follows:

```
sudo chmod -R 777 DVWA
```

Navigate to the config file in the installation folder, as follows:

```
cd DVWA/config
```

Copy the config file and rename it, as follows:

```
cp config.inc.php.dist config.inc.php
```

Open the config file to see the database credentials and modify the password to something easier to type (in the following example, I changed the password to pass):

```
sudo nano config.inc.php
```

The following screenshot shows the content of the config file, including all database information:

![](img/8c6a223c57e25ea0cc1593903a1b920f_365_0.png)

Figure 12-6 – DVWA database user configuration

Install mariadb by running the following commands:

```
sudo apt-get update
sudo apt-get -y install apache2 mariadb-server php
php-mysql php-gd libapache2-mod-php
```

Start the database by running the following command:

```
sudo service mysql start
```

- 9. Log in to the database (the password is blank, so just hit Enter when asked), as follows:

```
sudo mysql -u root -p
```

- 10. Now, we need to create a user in the database. In this case, we need to use the same username and password that we just created in the config file (see Figure 12.7). Here's the code you'll need:

- 11. Now, we need to grant all privileges to the user on the database, like this:

```
grant all privileges on dvwa.* to 'user'@'127.0.0.1' identified by 'pass';
```

> Tip Notice that since we are working on the database, those commands need to end with a semicolon (;).

- 12. Now, the result of those operations on the database should look like this:

```
kali@kali:~~$ sudo mysql -u root -p
Enterter password:
Welcome to the MariaDB monitor. Commands end with ; or \
Your MariaDB connection id is 5
Server version: 10.5.9-MariaDB-1 Debian build-unsigned

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation And others.

Type 'help' or '\h' for help. Type '\c' to clear the current input statement.
MariaDB ([#none]) create user 'dvwa'@'127.0.0.1' identified by 'pass'
Query OK, 0 rows affected (0.001 sec)
MariaDB ([#none]) grant all privileges on dvwa.* to 'dvwa'@'127.0.0.1'
Query OK, 0 rows affected (0.006 sec)
```

Figure 12.7 – Successful creation of the user on the database

- 13. Now is time to navigate to the apache2 directory to configure our Apache server, as follows:

```
cd /etc/php/7.3/apache2
```

- 14. Now, let's modify the php.ini file to ensure the following parameters are on: allow_url_fopen and allow_url_include, as shown in Figure 12.9, and to do that we will use mousepad, as follows:

```
sudo mousepad php.ini
```

Notice that the file is big, so you may need to scroll to the middle of the file to reach the fopen wrappers to modify these values, as illustrated in the following screenshot:

![](img/8c6a223c57e25ea0cc1593903a1b920f_367_0.png)

Figure 12.8 – Apache server parameters

- 15. Now, it is time to start the Apache server. You can do this by running the following command:

```
sudo service apache2 start
```

If everything went well, you should be able to open DWWA from your browser by typing the following in the address bar: 127.0.0.1/DWWA/.
Congratulations! You can see the same in the following screenshot, it means you have successfully installed DWWA:

![](img/8c6a223c57e25ea0cc1593903a1b920f_367_1.png)

Figure 12.9 – DWWA configuration page

Oh, but wait—there is still one more step. Scroll down and click on Create/Reset Database. This will create a database for you and after a few seconds, you will be directed to a login screen, as shown in the following screenshot:

![](img/8c6a223c57e25ea0cc1593903a1b920f_368_0.png)

Figure 12.10 – DVWA login screen

Now, just enter the following credentials to log in:

- admin
- password

As seen in the following screenshot, there are a lot of interesting vulnerabilities that you can test and experiment with, such as Brute Force, Command Injection, File Inclusion, SQL Injection, and more:

# Overlooking the most common attacks on web applications

![](img/8c6a223c57e25ea0cc1593903a1b920f_369_0.png)

Figure 12.11 – DVWA interface

One very interesting attack is the famous XSS attack, which we will review in the following section.

# Overlooking the most common attacks on web applications

Now is the time to talk about the most common attacks against web applications that you may face, and of course, all the methods, techniques, and tools you use to protect your systems against them.

# Exploring XSS attacks

The logic behind this type of attack is very simple: to leverage some JavaScript or HTML to execute code on your web application.

To better understand these types of attacks, let's look at one of the most common types of XSS attacks: the hijacking of user sessions.

# Hijacking a user session

Here, the attacker will try to inject malicious code into a web application that can be used to exfiltrate the session cookie that will be used to impersonate the victim.

To illustrate this attack, let's see an example based on a web application used to rent houses, as follows:

1. The attacker will log in to the vulnerable site and create an entry to advertise the renting of a house but inside the description field (which a normal person will use), the attacker will embed malicious code aimed at gathering the user's session cookie and sending it to their server.
2. When another user opens that hacked advertisement to rent a house, the malicious JavaScript will be executed and the victim's session cookie will be copied and sent to the attacker.
3. Now, the attacker can impersonate the victim by the stolen session cookie to identify themselves as the victim on the system, as shown in the following screenshot:

![](img/8c6a223c57e25ea0cc1593903a1b920f_370_0.png)

Now, let's see how you can prevent this attack. You could do the following:

- Set php.ini directives, as follows:

```
session.use_only_cookies = 1 -> for using only cookie based session ids
session.use_trans_sid = 0 -> disable showing PHPSESSID in browser url
```

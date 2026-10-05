
# INTRODUCTION 901

For example, installing phpmyadmin(sourceforge.net/projects/phpmyadmin) makes it available to a browser as /phpmyadmin.

This section describes the packages you need to install and provides references for the programs covered in this chapter. The “Notes” section introduces terminology and other topics that may help you make better sense of this chapter. The JumpStart section (page 903) gets Apache up and running as quickly as possible.

# MORE INFORMATION

- Local Apache HTTP Server Version 2.2 Documentation: With Apache running apache-2-doc installed, point a browser at server/manual, where server is localhost or the name or IP address of the Apache server.
- Apache directives: server/manual/mod/directives.html
- SSI directives: server/manual/howto/ssl.html
- Web Apache documentation: http.apache.org/docs/2.2
- Apache directives: http.apache.org/docs/2.2/mod/directives.html
- Apache Software Foundation (newsletters, mailing lists, projects, module registry, and more): www.apache.org
- webalizer: www.murunix.net/webalizer
- awstats: awstats.sourceforge.org
- libapache2-mod-perl: perl.apache.org (mod_perl)
- libapache2-mod-php5: www.php.net (mod_php)
- libapache2-mod-python: www.modpython.org (mod_python)
- SSL: modssl.org (mod_ssl)
- MRTG: mrtg.hartl/mrtg
- SNMP: net-snmp.sourceforge.net
- SSI directives: http.apache.org/docs/2.2/howto/ssl.html

# NOTES

- Terms: Apache and apache2 Apache is the name of a server that serves HTTP and other content. The name of Apache 2 daemon is apache2.
- Terms: server and process An Apache server is the same as an Apache process. An Apache child process exists to handle incoming client requests; it is referred to as a server.
- Firewall An Apache server normally uses TCP port 80; a secure server uses TCP port 443. If the Apache system is running or behind a firewall, you must open one or both of these ports. To get started, open port 80 (HTTP). Using gufw (page 876), open these ports by setting a policy that allows service for HTTP and or HTTPS.
- Running with root privileges Because Apache serves content on privileged ports, you must start running with privileges. For security reasons, Ubuntu sets Apache to spawn processes that run as the user and group www-data.
- Locale The apache2 daemon starts with the C locale by default. You can modify this behavior—for example, by using the configured system locale—setting the LANG variable in the /etc/init.d/apache2 file. (in the line that starts with ENV=-i LANG= ...) in the /etc/init.d/apache2 file.

The root of the directory hierarchy Apache serves content from is called the document root and is controlled by the DocumentRoot directive (page 913). This directive defines a directory on the server that maps to /. This directory appears to users who are browsing a Web site as the root directory. As distributed by Ubuntu, the document root is /var/www.

Modifying content with the default Ubuntu configuration of Apache, only a user with root privileges can add or modify content in /var/www. To avoid people work as root when they are manipulating content, create a group (webwork, for example), but people need to work with Web content in this group, and make the directory hierarchy starting at /var/www (another document root) writable by that group. In addition, if you give the directory set permission, all new files created within this hierarchy will belong to the group, which facilitates sharing files. The first three commands below add the new group, change the mode of the document root to setgid, and change the group that the document belongs to. The last command adds username to the webwork group; you must repeat this command for each user you want to add to the group.

```
$ sudo addgroup webwork
$ chmod g+s /var/www
$ sudo chown :webwork /var/www
```

See page 597 for more information about working with groups.

runs Apache version 2.2.

# RUNNING A WEB SERVER (APACHE)

This section explains how to install, test, and configure a basic Web server.

# PREREQUISITES

Minimal installation Install the following package:

- apache2

apache2 init script When you install the apache2 package, the dpkg postinst script starts the apache2 daemon. After you configure Apache, call the apache2 init script to restart the apache2 daemon.

```
$ sudo service apache2 restart
```

After changing the Apache configuration on an active server, use reload in place of restart reload Apache configuration files without disturbing clients connected to the server.

Optional packages The mod_ssl package is installed as part of the apache2 package—you do not need to install it separately. You may want to install the following optional packages:

- apache2-doc—The Apache manual
- webalizer—Web server log analyzer (page 948)
- awstats—Web server log analyzer
- libapache2-mod-perl2—Embedded Perl scripting language (mod_perl)
- libapache2-mod-python—Metackage that installs the embedded Python scripting language (mod_python)
- libapache2-mod-php5—Embedded PHP scripting language, including IMAP and LDAP support (mod_php)
- mrtg—MRTG traffic monitor (page 948)

**The apache2ctl utility for restarting Apache**

> tip The apache2 init calls apachectl to start and stop Apache. The reload argument calls this utility with argument of *graceful*, which does not disturb clients that are connected to the server. The *restart* and *force-reload* arguments call it with arguments of *stop* and then *start*; pair of commands shuts down the server completely before restarting it.

# JUMPSTART: GETTING APACHE UP AND RUNNING

To get Apache up and running, modify the `/etc/apache2/sites-available/default` configuration file as described in this section. *Directives I: Directives You May Want to Modify as You Get Started* on page 910 explains more about this file and explores other changes you may want to make to it.

# MODIFYING THE CONFIGURATION FILES

Apache runs as installed, but it is a good idea to add the three lines described in this section to the /etc/apache2/sites-available/default file. The ServerName establishes the name of the server. Add one of the following lines to restart Apache (page 902).

```
ServerName example.com
```

or

```
ServerName IP_address
```

where example.com is the domain name and the IP_address is the IP address of the server. If you do not have a domain name, use the IP address. Add these lines to the /etc/apache2/sites-available/default file.

```
ServerAdmin email_address
ServerSignature EMail
```

email_address is the email address of the person who needs to know when people are using the server. Make sure that someone checks this email account frequently. But also see the tip “ServerAdmin” on page 912.

It can make system administration much easier if you use a role alias (for example, webmaster@example.com) instead of a specific username (e.g., max@example.com) as an email_address. See the discussion of email aliases on page 722.

After making the changes to the file default, restart apache2 as explained on page 902.

# TESTING APACHE

Once you restart the apache2 daemon, you can confirm that Apache is working correctly by pointing a browser to the local (server) system to http://localhost/. From a remote system, point a browser to http:// followed by the ServerName you specified in the previous section. If you are displaying a page from a system other than the local one, the local system must know how to resolve the domain name you enter (e.g., using DNS or the /etc/hosts file). For example, you might use either of these URI formats: http://192.168.0.16 or http://example.org.

When you point a browser to a directory that holds a file index.html, Apache causes the browser to display the contents of that file (otherwise it displays a directory listing). In response to your request, the browser should display the page stored at /var/www/index.html on the server. In this case, the browser should display!

If the server is behind a firewall, open TCP port 80 (page 901). If you are having problems getting Apache to work, “Troubleshooting” on page 940.

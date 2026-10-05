
## 732 CHAPTER 20 exim4: SETTING UP MAIL SERVERS, CLIENTS, AND MORE

### Installation
Install the following packages:

- squirrelmail
- apache2 (page 902; installed as a dependency when you install squirrelmail)
- exim4 (page 714) or sendmail
- php5-cgi
- dovecot-imapad (page 735) or another IMAP server

### Startup
You do not need to start SquirrelMail, nor do you have to open any ports for it. However, you need to configure, start, and open ports (if the server is running on a system with a firewall) for exim4 (page 718), IMAP (page 735), and Apache (page 903).

### Configuration
The SquirrelMail files reside in /usr/share/squirrelmail. Create the following link to make SquirrelMail accessible from the Web:

```
$ sudo ln -s /usr/share/squirrelmail /var/www/mail
```

Give the following command to configure SquirrelMail:

```
$ sudo squirrelmail-configure
SquirrelMail Configuration : Read: config.php (1.4).0
```

```
+ Main Menu =
1. Organization Preferences
2. Server Settings
3. Folder Defaults
4. General Options
5. Themes
6. Address Books
7. Message of the Day (MOTD)
8. Plugins
9. Database
10. Languages

- D Set pre-defined settings for specific IMAP servers
- D Turn color on
- S Save data
- Q Quit

```

This menu has multiple levels. When you select a setting (and not submenu), squirrelmail-configure displays information that can help decide how to answer the question it poses. Set the server's domain name (number 1 on the Server Settings page) and the name of the IMAP server you are using (D on the main menu). SquirrelMail provides several themes; if you do not like the SquirrelMail looks, choose another theme from Themes (number 5). When you are finished making changes, exit from squirrelmail-configure. Run squirrelmail-configure whenever you want to change the configuration of SquirrelMail.

SquirrelMail provides a Web page that tests its configuration. Point a browser on the server at localhost/src/configtest.php. Replace localhost with the IP address or

![](img/45ff4cd21497435daa35084a84b95d07_782_0.png)

## ADDITIONAL EMAIL TOOLS 733

![](img/45ff4cd21497435daa35084a84b95d07_783_0.png)

# Figure 20-2 SquirrelMail running a configuration test

FQDN of the server to view the page from another system. SquirrelMail checks its configuration and displays the results on this page. Figure 20-2 shows that SquirrelMail cannot connect to the IMAP server on the local system, probably because IMAP has not been installed.

In a web browser at localhost/ or localhost/mail/src/login.php to display the SquirrelMail login page (Figure 20-3). Replace localhost with the IP address or password of a user who has an account on the server system.

## MAILING LISTS

A mailing list can be an asset if you regularly send email to the same large group of people. It offers several advantages over listing numerous recipients in the To or Cc field of email or sending the same email to many people:

- Anonymity—None of the recipients of the email can see the addresses of the other recipients.

![](img/45ff4cd21497435daa35084a84b95d07_783_1.png)

# Figure 20-3 SquirrelMail login page

## 734 CHAPTER 20 exim4: Setting UP MAIL SERVERS, CLIENTS, AND MORE

- Archiving—Email sent to the list is stored in a central location where list members or the public, as specified by the list administrator, can browse through it.
- Access control—You can specify who can send email to the list.
- Consistency—When you send mail to a group of people using To or Cc, it is easy to forget who wants to be on the list and erroneously include people who want to be off the list.
- Efficiency—A mailing list application spreads email transmissions over time it does not overload the mail server.

Mailman, the GNU list manager, is written in Python and manages email discussions and newsletter lists. Because it is integrated with the Web, Making it easy for users to manage their accounts and for administrators to manage lists. See the Mailman page (www.list.org) and the files in the /usr/share/doc/mailman directory for more information.

### Prerequisites
Install the mailing package and an MTA such as exim4 (page 715). To use the Web interface you must install Apache (page 902).

### Installing
When you install the mailman package, the dpkg postinst script describes a graphical interface that asks you to specify the language you want Mailman to display and tells you that you must create a list. Give the following request for painting_class:

```
$ sudo new painting_class
Enter the email of the person running the list: helen@example.com
Initial painting_class password:
```

To finish creating your mailing list, you must edit /etc/aliases (or equivalent) file by adding the following lines, and possibly running the 'newaliases' program:

```
## painting_class mailing list
paintingclass: "/var/lib/mailman/mailman painting_class"
paintingclass-admin: "/var/lib/mailman/mailman admin painting_class"
paintingclass-bounces: "/var/lib/mailman/mailman bounces painting_class"
paintingclass-confirm: "/var/lib/mailman/mailman confirm painting_class"
paintingclass-join: "/var/lib/mailman/mailman join painting_class"
paintingclass-leave: "/var/lib/mailman/mailman leave painting_class"
paintingclass-owner: "/var/lib/mailman/mailman owner painting_class"
paintingclass-request: "/var/lib/mailman/mailman request painting_class"
paintingclass-subscribe: "/var/lib/mailman/mailman subscribe painting_class"
paintingclass-unsubscribe: "/var/lib/mailman/mailman unsubscribe painting_class"
```

Hit enter to notify painting_class owner...

Before users on the list can receive email, you need to copy the newlist (the ones that start with the name of your mailing list) to the end of /etc/aliases (page 722) and run newaliases (page 723).

### mailman site list
Before you start Mailman, you must create a site list named mailman. Give the command sudo newlist mailman, copy the lines to the aliases file, and run newaliases.

## ADDITIONAL EMAIL TOOLS 735

### mailman init script
After setting up the mailman site list and a site list of your choice, start the Mailman qrunner daemon with the following command:

```
$ sudo service mailman start
* Starting Mailman master qrunner mailmanctl [ OK ]
```

After modifying any Mailman configuration files or adding a new site list, the same command, replacing start with reload, cause Mailman to reread its configuration files.
The main Mailman configuration file is /etc/mailman/mm_cfg.py. When you install Mailman, it automatically assigns values to DEFAULT_EMAIL_HOST (the default domain for mailing lists) and DEFAULT_URL_HOST (the default web server for Mailing). Change the value of these variables and restart Mailman.

```
$ cat /etc/mailman/mm_cfg.py
...
# Default domain for email addresses of newly createds
DEFAULT_EMAIL_HOST = 'example.com'

# Default host for web interface of newly createds
DEFAULT_URL_HOST = 'example.com'
```

Assuming that the Web interface is for example.com, anyone can point a browser to example.com/cgi-bin/mailman/listinfo to display a list of mailing lists. Click the name of a mailing list to display a page that allows you to view the list' archives, send, or subscribe to the list. At the bottom of the page is a link to the administrative interface for the list.

## SET UP AN IMAP OR POP3 MAIL SERVER

Dovecot IMAP (Internet Message Access Protocol) and POP (Post Office Protocol) allow users to retrieve and manipulate email remotely. This explanation covers how to set up servers for these protocols. Dovecot (dovecot.org and wiki.dovecot.org) provides the imap-login and pop3-login daemons that implement these protocols.

### Prerequisites
Install the dovecot-pop3 (for a POP3 server) and/or dovecot-imap (for an IMAP server) packages. APT installs the dovecot-common package automatically when you install one of packages. When you install either package, the dpkg postinst script for the dovecot-common package generates self-signed SSL certificates if they do not exist.

### Configuration
Dovecot will not start until you specify in the /etc/dovecot/dovecot.conf file servers you want to run. Near the beginning of this long file is a line that starts with protocols =\ The names of the servers you want to run at the end of this line. Possible servers, depending on which packages you have installed, imap (IMAP on port 143), imaps (IMAP over SSL on port 993), pop3 (POP3 on port 110), and pop3s (POP3 over SSL on port 995).

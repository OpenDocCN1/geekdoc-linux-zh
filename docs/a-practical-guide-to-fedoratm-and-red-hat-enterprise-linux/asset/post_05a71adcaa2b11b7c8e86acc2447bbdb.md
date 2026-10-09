
![](img/243613168ac865b539f12460d966088e_816_0.png)

Figure 20-3 SquirrelMail running a configuration test

## Startup
You do not need to start SquirrelMail, nor do you have to open any ports for it. However, you need to configure, start, and open ports (if the server is running on a system with a firewall) for sendmail (page 743), IMAP (page 763), and Apache (page 936).

## Configuration
The SquirrelMail files reside in /usr/share/squirrelmail. Create the following link to make SquirrelMail accessible from the Web:

```
# ln -s /usr/share/squirrelmail /var/www/html/mail
```

Give the following commands to configure SquirrelMail:

```
# cd /usr/share/squirrelmail/config
# ./conf.pl
SquirrelMail Configuration : Read: config_default.php (1.4.0)

Main Menu --
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
D. Set pre-defined settings for specific IMAP servers
C Turn color on
S Save data
Q Quit

Command >>
```

This menu has multiple levels. When you select a setting (and not a submenu), conf.pl displays information that can help you decide how to answer the question it poses. Set the server's domain name (number 1 on the Server Settings page) and the name of the IMAP server you are using (D on the main menu). SquirrelMail provides several themes; if you do not like the way SquirrelMail looks, choose another theme from Themes (number 5). When you are finished making changes, exit from `conf.pl`. Run `conf.pl` whenever you want to change the configuration of SquirrelMail.

![](img/243613168ac865b539f12460d966088e_817_0.png)

Figure 20-4 SquirrelMail login page

SquirrelMail provides a Web page that tests its configuration. Point a browser on the server at `localhost/mail/src/conf/test.php`. Replace `localhost` with the IP address or FQDN of the server to view the page from another system. SquirrelMail checks its configuration and displays the results on this page. Figure 20-3 shows that SquirrelMail cannot connect to the IMAP server on the local system, probably because IMAP has not been installed.

## Logging in
Point a Web browser at `localhost/mail` or `localhost/mail/src/login.php` to display the SquirrelMail login page (Figure 20-4). Replace `localhost` with the IP address or FQDN of the server to view the page from another system. Enter the username and password of a user who has an account on the server system.

# MAILING LISTS

A mailing list can be an asset if you regularly send email to the same large group of people. It offers several advantages over listing numerous recipients in the To or Cc field of an email or sending the same email individually to many people:

- Anonymity—None of the recipients of the email can see the addresses of the other recipients.
- Archiving—Email sent to the list is stored in a central location where list members or the public, as specified by the list administrator, can browse through it.
- Access control—You can specify who can send email to the list.
- Consistency—When you send mail to a group of people using To or Cc, it is easy to forget people who want to be on the list and to erroneously include people who want to be off the list.
- Efficiency—A mailing list application spreads email transmissions over time so it does not overload the mail server.

| Item | Description |
| :--- | :--- |
| **Mailman** | Mailman, the GNU list manager, is written mostly in Python and manages email discussions and email newsletter lists. Because it is integrated with the Web, Mailman makes it easy for users to manage their accounts and for administrators to manage lists. For more information, see the Mailman home page (www.list.org) and, once you have installed Mailman, the files in the /usr/share/doc/mailman* directory. |
| **Prerequisites** | Install the **mailman** package and an MTA such as **sendmail** (page 742). To use the Web interface you must install Apache (page 935). |
| **Mailman site list** | Give the following **newlist** command to create a site list, substituting the name of your mailing site for *painting_class*. You must also create a site list named **mailman** (substitute **mailman** for *painting_class*); otherwise Mailman will not start. |

```
# /usr/lib/mailman/bin/newlist
Enter the name of the list: painting_class
Enter the email of the person running the list: helen@example.com
Initial painting_class password:
```

To finish creating your mailing list, you must edit your /etc/aliases (or equivalent) file by adding the following lines, and possibly running the *newaliases* program:

```
## painting_class mailing list
painting_class:	"/usr/lib/mailman/mail/mailman post painting_class"
painting_class-admin:	"/usr/lib/mailman/mail/mailman admin painting_class"
painting_class-bounces:	"/usr/lib/mailman/mail/mailman bounces painting_class"
painting_class-confirm:	"/usr/lib/mailman/mail/mailman confirm painting_class"
painting_class-join:	"/usr/lib/mailman/mail/mailman join painting_class"
painting_class-leave:	"/usr/lib/mailman/mail/mailman leave painting_class"
painting_class-owner:	"/usr/lib/mailman/mail/mailman owner painting_class"
painting_class-request:	"/usr/lib/mailman/mail/mailman request painting_class"
painting_class-subscribe:	"/usr/lib/mailman/mail/mailman subscribe painting_class"
painting_class-unsubscribe:	"/usr/lib/mailman/mail/mailman unsubscribe painting_class"
Hit enter to notify painting_class owner...
```

Before users on the list can receive email, you need to copy the lines generated by **newlist** (the ones that start with the name of the new mailing site) to the end of /etc/aliases (page 746) and run **newaliases** (page 747).

> **Tip:** You must use the **newlist** utility to create a site list named **mailman** in addition to the site lists you want to set up. If you do not create this site list, you will not be able to start Mailman.

| Item | Description |
| :--- | :--- |
| **mm_cfg.py** | The main Mailman configuration file is /etc/mailman/mm_cfg.py. When you install Mailman, it assigns the value of *fqdn* to DEFAULT_EMAIL_HOST (the default domain for mailing lists) and **DEFAULT_URL_HOST** (the default Web server for Mailman) in this file. Change the values assigned to these variables as needed, making sure to enclose the values within single quotation marks, and start or restart Mailman. The following example uses www.example.com as the default Web server and mail.example.com as the default mail server: |

```
# grep '^DEFAULT' /etc/mailman/mm_cfg.py
DEFAULT_URL_HOST = 'www.example.com'
DEFAULT_EMAIL_HOST = 'mail.example.com'
```

You can configure many aspects of Mailman mailing lists by modifying the file named `/etc/mailman/sitelist.cfg`. See the comments in this file for more information.

After setting up the **mailman** site list and a site list of your choice, run `systemctl` to start the **mailman** service when the system enters multiuser mode and then start the **mailman** service. Use the `systemctl status` command to make sure the service is running.

```
# systemctl enable mailman.service
# systemctl start mailman.service
```

After modifying any Mailman configuration files or adding a new site list, give the second command again, replacing **start** with **restart** to cause Mailman to reread its configuration files. Remember also to start **sendmail** and **Apache** as needed.

You must modify the last line of the `/etc/httpd/conf.d/mailman.conf` file before the Mailman Web interface will work. Remove the leading **hashmark** ( **#**) and change the domain name to that of the host for the Web interface as previously established in `mm_cfg.py`:

```
# tail -1 /etc/httpd/conf.d/mailman.conf
RedirectMatch ^/mailman/.*)$ http://www.example.com/mailman/listinfo
```

Restart **Apache**. Assuming the host for the Web interface is `example.com`, anyone can point a browser at `example.com/mailman` to display a list of available mailing lists. Click the name of a mailing list to display a page that allows you to view the list's archives, send a message, or subscribe to the list. At the bottom of the page is a link to the administrative interface for the list.

If Mailman indicates that there are no publicly-advertised Mailman mailing lists, add the following line to `mm_cfg.py` and restart Mailman.

```
VIRTUAL_HOST_OVERVIEW = Off
```

# SETTING UP AN IMAP OR POP3 MAIL SERVER

**Dovecot** IMAP (Internet Message Access Protocol) and POP (Post Office Protocol) allow users to retrieve and manage email remotely. This section explains how to set up servers for these protocols. **Dovecot** (www.dovecot.org and wiki.dovecot.org) implements these protocols. After you install **Dovecot**, see `/usr/share/doc/dovecot*` for more information.

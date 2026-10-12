
## OpenGroupware (Formerly SKYrix 4.1)

OpenGroupware (not affiliated with OpenOffice.org) focuses on groupware and collaboration (and does not provide its own mail server). It can replace Comfire in SuSE OpenExchange to save on the licensing cost or be used with a Cyrus-imap mail server and PostgreSQL and FrontBase (no MySQL) for the database. For connectivity to Outlook, OpenGroupware uses the ZedeLook MAP I Storage Provider (proprietary, it maps MAP I to WebDAV) and the Open Source WebDAV middleware server ZideStore. ZideStore translates WebDAV requests to calls to OpenGroupware as well as clients such as Evolution and Mozilla. The home page is http://www.opengroupware.org/en/.

## phpgroupware

phpgroupware is an open source application written in PHP (and used with MySQL or postgresql plus a web server and an IMAP mail server). phpgroupware provides a web-based calendar, task list, address book, email, news headlines, and a file manager. The home page is http://www.phpgroupware.org/.

## PHPprojekt

PHPprojekt is open source software written in PHP (used with MySQL, postgresql, Oracle, Informix, or MS-SQL). PHPprojekt provides calendaring, contact manager, time card system, project management, online chat, threaded discussion forum, trouble ticket system, email, public files, notes bookmarks, voting system, task lists, reminders, site-search, and integration with the PostNuke news site application. It provides no Exchange/ Outlook compatibility whatsoever. The home page is http://www.PHPprojekt.com/.

## IMP/ Horde

IMP/ Horde is a PHP-based application framework. When combined with an HTTP server (Apache, Microsoft IIS, Netscape) and MySQL database, IMP/ Horde offers modules that provide webmail, contact manager, calendar, CVS viewer, file manager, time tracking, email filter rules manager, notes, tasks, chat, newsgroups, forms, bug tracking, FAQ repository, and presentations. The home page is http://www.horde.org/.

## Conclusion

There are no open-source-only alternatives that can provide full Exchange-like services to MS Outlook clients. If you do not have Outlook clients to worry about, OpenGroupware, IMP/ Horde and phpprojekt look promising. None of them are provided with Fedora.

## RELEVANT FEDORA AND LINUX COMMANDS

You will use the following commands to manage electronic mail in Fedora:

- balsa— A GNOME mail user agent for X
- biff— A console-based mail notification utility
- evolution— A comprehensive and capable Ximian GNOME mail PIM for X
- fetchmail— A console-based and daemon-mode mail retrieval command for Linux
- fetchmailconf— A graphical fetchmail configuration client for X
- kmail— A graphical mail user client for KDE and X
- kedit— A mail applet for KDE and X
- mail— A console-based mail user agent
- mutt— A console-based mail user agent
- sendmail— A comprehensive mail transport agent for UNIX and Linux
- xbiff— A mail notification X client

## Reference

The following references are recommended reading for email configuration. Of course, not all references apply to you. Select the ones that apply to the email server that you are using.

### Web Resources

- http://www.sendmail.org/— This is the Sendmail home page. Here you can find configuration information and FAQs regarding the Sendmail MTA.
- http://www.postfix.org/— This is the Postfix home page. If you are using the Postfix MTA, documentation and sample configurations can be found at this site.
- http://www.qmail.org/— This is the home page for the Qmail MTA. It contains documentation and links to other resources on Qmail.
- http://www.linuxgazette.com/issue/35/ac.html— IMAP on Linux: A Practical Guide. The Internet Mail Access Protocol allows a user to access his email stored on a remote server rather than a local disk.
- http://www.redhat.com/support/resources/faq/RH-postfix-FAQ/book1.html— A slightly out-of-date but still very useful HOWTO about setting up Postfix in a Red Hat environment.
- http://www.imap.org/about/whatisIMAP.html— A page describing what IMAP is.
- http://www.rfc-editor.org/— A repository of RFCs— Request for Comments— that define the technical “rules” of modern computer usage.
- http://www.procmail.org/— The Procmail homepage.
- http://www.moongroup.com/docs/procmail/— The Procmail FAQ, which includes suggestions for troubleshooting problems. The page also references a page of links that, in turn, reference other link collections as well as tidbits from the Procmail mail list.
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/Other-formats/html_single/Qmail-VxMailMgr-Courier-imap-HOWTO.html— if you want some help configuring a mail system based on the lesser-used applications, this HOWTO can help.

### Books

*Sendmail* from O'Reilly Publishing. This is the de facto standard guide for everything Sendmail. It is loaded with more than 1,000 pages, which gives you an idea of how complicated Sendmail really is.

*Postfix* from Sams Publishing. An excellent book that covers the Postfix MTA.

*Running Qmail* from Sams Publishing. This is similar to the Postfix book from Sams Publishing except that it covers the Qmail MTA.

## CHAPTER 26

## Setting Up a Proxy Server

There are two things in this world that you can never have enough of: time and bandwidth. Fedora comes with a proxy server— Squid— that enables you to cache web traffic on your server so that websites load faster and users consume less bandwidth.

### What Is a Proxy Server?

A proxy server lies between client machines— the desktops in your company— and the Internet. As clients request websites, they do not connect directly to the Web and send the HTTP request. Instead, they connect to the local proxy server. The proxy then forwards their request on to the Web, retrieves the result, and hands it back to the client. At its simplest, a proxy server really is just an extra layer between client and server, so why bother?

The three main reasons for deploying a proxy server are

- **Content control**— You want to stop people whiling away their work hours reading the news or downloading MP3s.
- **Speed**— You want to cache common sites to make the most of your bandwidth.
- **Security**— You want to monitor what people are doing.

Squid is capable of achieving all of these goals and more.

### IN THIS CHAPTER

- What Is a Proxy Server?
- Installing Squid
- Configuring Clients
- Access Control Lists
- Specifying Client IP Addresses
- Sample Configurations
- Reference

### Installing Squid

Squid installation is handled through the Add/Remove Software dialog. The Squid package is confusingly located under the Web Server group; this has the downside of installing Apache alongside Squid whether you like it or not. That said, you can (and should) deselect other autostart packages that you do not need from the Web Server category.

After Squid is installed, switch to the console and use su to get to the root account. You should run the command `chkconfig --level 345 squid on` to run Squid at runlevels 3, 4, and 5, like this:

```
[root@susannah ~]# chkconfig --list squid
squid     0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root@susannah ~]# chkconfig --level 345 squid on
[root@susannah ~]# chkconfig --list squid
squid     0:off 1:off 2:off 3:on 4:on 5:on 6:off
```

That runs Squid the next time the system switches to runlevel 3, 4, or 5, but it will not run it just yet.

### Configuring Clients

Before you configure your new Squid server, you should set up the local web browser to use Squid for its web access. This allows you to test your rules as you are working with the configuration file.

To configure Firefox, select Preferences from the Edit menu. From the dialog that appears, click the Connection Settings button (near the bottom on the General tab) and select the option Manual Proxy Configuration. Check the box beneath it, Use the Same Proxy for All Protocols; then enter 127.0.0.1 as the IP address and 3128 as the port number. See Figure 26.1 for how this should look. If you are configuring a remote client, specify the IP address of the Squid server instead of 127.0.0.1.

For Konqueror, go to the Settings menu and select Configure Konqueror. From the left tab, scroll down to Proxy, select Manually Specify the Proxy Settings, and then click Setup. Enter 127.0.0.1 as the proxy IP address and 3128 as the port. As with Firefox, if you are configuring a remote client, specify the IP address of the Squid server instead of 127.0.0.1.

Internet Explorer's proxy settings are in Tools/Internet Options. From the Connections tab, click the LAN Settings button and enable the Use a Proxy Server for Your LAN option. Enter the address as the IP of your Squid machine, and then specify 3128 as the port.

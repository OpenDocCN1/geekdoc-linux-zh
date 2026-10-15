

Several “drop-in” alternatives exist, none of which are fully open source because some type of proprietary connector is needed to provide the services to Microsoft Outlook clients (or provide Exchange services to the Linux Evolution client). For Outlook compatibility, the key seems to be the realization of a full, open implementation of MAPI, the Microsoft Messaging Application Program Interface. That goal is going to be difficult to achieve because MAPI is a poorly documented Microsoft protocol. For Linux-only solutions, the missing ingredient for many alternatives is a usable group calendaring/scheduling system similar in function to that provided by Exchange Server/Outlook.

Of course, independent applications for these functions abound in the open-source world, but one characteristic of “groupware” is its central administration; another is that all components can share information.

The following sections examine several of the available servers, beginning with Microsoft Exchange Server itself and moving toward those applications that have increasing incompatibility with it. None of these servers are provided with Ubuntu.

## Microsoft Exchange Server/Outlook Client

Exchange Server and Outlook seem to be the industry benchmark because of their widespread deployment. They offer a proprietary server providing email, contacts, scheduling, public folders, task lists, journaling, and notes using Microsoft Outlook as the client and MAPI as the API. If you consider what Microsoft Exchange offers as the “full” set of features, no other replacement offers 100% of the features exactly as provided by Microsoft Exchange Server—even those considered “drop-in” replacements. The home page for the Microsoft Exchange server is http://www.microsoft.com/exchange/.

## CommuniGate Pro

CommuniGate Pro is a proprietary, drop-in alternative to Microsoft Exchange Server, providing, email, webmail, LDAP directories, a web server, file server, contacts, calendaring (third party), and a list server. The CommuniGate Pro MAPI Connector provides access to the server from Microsoft Outlook and other MAPI-enabled clients. The home page for this server is http://www.stalker.com/.

## Oracle Collaboration Suite

This is probably the closest that you will get to an Exchange replacement, allowing you to collaborate by instant messaging, email, sharing files (workspaces), calendaring, and other tools. It provides an Outlook Connector for users who have to have the familiarity of Outlook. OCS is available for Linux platforms and its homepage is http://www.oracle.com/collabsuite/.

## Bynari

Bynari provides a proprietary group of servers to act as a drop-in replacement for Microsoft Exchange Server for email, calendaring, public folders, scheduling, address book, webmail, and contacts. Although it runs on Linux, it offers no Linux clients, and the connector provides services to Microsoft Outlook only. The home page is http://www.bynari.net/.

## Open-Xchange

Open-Xchange has a great pedigree having been owned and developed by Novell/SUSE until being spun off by itself into its own company. Working with open standards, it provides a number of collaboration options and is firmly based on Linux. It can work with a wide variety of protocols, making it one of the best connected suites available. You can get the open source version at http://www.open-xchange.org.

## phpgroupware

phpgroupware is an open-source application written in PHP (and used with MySQL or postgresql plus a web server and an IMAP mail server). phpgroupware provides a web-based calendar, task list, address book, email, news headlines, and a file manager. Its modular nature enables you to plug in various components (around 50 at the last count) as you need them. The home page is http://www.phpgroupware.org/.

## PHProjekt

PHProjekt is open-source software written in PHP (used with MySQL, postgresql, Oracle, Informix, or MS-sql). PHProjekt provides calendaring, contact manager, time card system, project management, online chat, threaded discussion forum, trouble ticket system, email, public files, notes bookmarks, voting system, task lists, reminders, site search, and integration with the PostNuke news site application. It provides no Exchange/Outlook compatibility whatsoever. The home page is http://www.PHProjekt.com/.

## Horde

Horde is a PHP-based application framework. When combined with an HTTP server (Apache, Microsoft IIS, Netscape) and MySQL database, IMP/Horde offers modules that provide webmail, contact manager, calendar, CVS viewer, file manager, time tracking, email filter rules manager, notes, tasks, chat, newsgroups, forms, bug tracking, FAQ repository, and presentations. The home page is http://www.horde.org/.

## Relevant Ubuntu and Linux Commands

You will use the following commands to manage electronic mail in Ubuntu:

- `balsa`—A GNOME mail user agent for X
- `biff`—A console-based mail notification utility
- `evolution`—A comprehensive and capable Ximian GNOME mail PIM for X
- `fetchmail`—A console-based and daemon-mode mail retrieval command for Linux
- `fetchmailconf`—A graphical fetchmail configuration client for X
- `kmail`—A graphical mail user client for KDE and X
- `korn`—A biff applet for KDE and X
- `mutt`—A console-based mail user agent



![](img/b852150740856958b10aff9e8c9d2adc_124_0.png)

As mentioned earlier, Ximian Evolution also comes with an integrated calendar, task manager, and address book that makes mail and schedule management on Red Hat Linux 9 simple and intuitive.

## Accessing Microsoft Exchange Mail from Ximian

Several corporations use Microsoft Exchange as a groupware server, that is, a server that allows users to manage and share calendar events, contacts, e-mail, and even files. Unfortunately, the Exchange server is designed to work primarily with Microsoft Outlook and quite often it is not configured to allow clients to access e-mail using the POP or IMAP protocols. However, Ximian provides a commercially licensed connector to access e-mail from an Exchange server. It should be noted that if POP access is enabled, the connector is not required if we use the Microsoft Exchange server only for e-mail. We definitely need the connector if we rely on a Microsoft Exchange server for calendar and file-sharing features.

> The Ximian connector can be downloaded from http://www.ximian.com. To install the connector, we need to also download Red Carpet, the Ximian installer, from the same web site.

To configure Ximian to retrieve and send mail using an Exchange server, from the **Tools | Mail Settings** menu we set the *Server Type* as *Microsoft Exchange* and supply the following information:

- 1. The mail user's full name.
- 2. The login name for the Exchange server. This is usually the part of the e-mail ID preceding the @ symbol, also known as the mail user ID. It may also be a different name altogether, depending upon how this is configured locally. Some installations have multiple NT domains, in which case the login name is of the format `domainname\login name`.
- 3. If the mail user ID is different from the login name, we need to provide that id as the mailbox name. In any case, there is no need to prefix the domain name.
- 4. The DNS name of the Exchange server, for example *exchange.foo bar.com*.
- 5. If an LDAP-based corporate directory server such as the *Netscape Directory Server* is deployed locally, the DNS name of the server can be entered to look up contacts using LDAP. LDAP stands for Lightweight Directory Access Protocol.

> If you're unsure about any of this information, you should speak to whoever is responsible for the running of your Exchange Server.

## The Mozilla Mail Client

The Mozilla mail client is fast gaining popularity as a fully featured mail client. It has several features for managing multiple e-mail accounts and most importantly news accounts. For users who subscribe to news groups besides accessing e-mail, the Mozilla client is an excellent choice. The Mozilla client can be started from **Main Menu | Internet | More Internet Applications | Mozilla mail** or by clicking the mail icon (bottom, left) of the Mozilla browser:

![](img/b852150740856958b10aff9e8c9d2adc_125_0.png)

When the Mozilla mail client is started for the first time, it prompts us to set up an account for sending and receiving e-mail. Also, a new account can be set up from the Edit | Mail & Newsgroups settings menu by clicking on the Add account button. In either case, the settings are similar to the settings for the Ximian Evolution client that we saw in the previous section. The news reader client can be set up from the same menu by specifying the new account as a Newsgroup account and entering the DNS name of the news server:

![](img/b852150740856958b10aff9e8c9d2adc_126_0.png)

## Switching Mail Transfer Agents

Mail transfer agents (MTAs) relay outgoing mail to its destination using the SMTP protocol. If you're using either of the mail clients that we've mentioned in this chapter, then you don't need to worry about them too much, as they're not involved in sending your mail. However, for completeness, you should know that they're there, and what they do.

Red Hat Linux 9 comes with a choice of two mail transfer agents, Sendmail and Postfix. The Mail Transfer Agent Switcher tool can be accessed from the Main Menu | System Settings | Mail Transfer Agent Switcher. We can switch the MTA to be used, by clicking the appropriate radio button and then selecting Apply.

Sendmail (official site [http://www.sendmail.org](http://www.sendmail.org)) is the oldest and therefore the most time-tested of the MTAs. It is easily the most popular mail transfer agent, delivering more than half of all the e-mail on the Internet. However, Sendmail has numerous security and performance issues owing to its age. Several new MTAs have emerged to take its place, improving upon the security aspects, performance, and ease of configuration. Postfix (official site [http://www.postfix.com](http://www.postfix.com)) is an MTA focused on better security and easier configuration. Exim (official site [http://www.exim.org](http://www.exim.org)) and qmail (official site [http://www.qmail.org](http://www.qmail.org)) are other popular MTAs. Most of the time Sendmail will work very well as the default MTA, but if we intend to do some serious re-configuration, Postfix might make the task much easier.

The important thing to note is that if we are using a mail client like Mozilla or Evolution, then the outgoing mail is sent directly to a mail server using SMTP. In this case, an MTA is not involved and it can be left alone with little impact. However, some older mail clients such as UNIX mail and some programs that send notification e-mail may require the MTA to be configured and enabled.

## Other Software

In this section we shall look at the other software beside browsers and mail clients that we can use to access the Internet.

## FTP Clients

We often need to download software over the Internet or transfer files between machines. The most popular protocol for this function is FTP or the File Transfer Protocol.

The gFTP tool (Graphical FTP) available with Red Hat Linux 9 installations is a graphical FTP tool that has several power features lacking in the other clients. The gFTP client can be started from the Main Menu | Internet | More Internet Applications | gFTP, or by typing `gftp` at the command line:

![](img/b852150740856958b10aff9e8c9d2adc_127_0.png)

The gFTP client is multi-threaded, allowing transfer of multiple files simultaneously, and supports transferring files between two remote servers over FTP (that is, not onto the machine you're working on). It also supports downloading entire directories and subdirectories, as well as being able to bookmark FTP sites allowing you to quickly reconnect to remote sites. gFTP also supports resuming interrupted file transfers.

Traditionally the most popular FTP client has been the command-line FTP tool, simply called `ftp`. The command-line tool is interactive and suitable for quickly fetching a file or two.

## Xchat

IRC or Internet Relay Chat is the predecessor of peer-to-peer and instant messaging systems of today. Owing to its huge user base, it is still one of the major reasons people connect to the Internet. Red Hat Linux 9 comes with an IRC client called Xchat that can be accessed from the Main Menu | Internet | More Internet Applications | Xchat menu:

![](img/b852150740856958b10aff9e8c9d2adc_128_0.png)

IRC consists of *channels* that are essentially topics of discussion, similar to the *chat room* of today's messaging clients. To join a channel we need to connect to a server that hosts the channel. We can choose a server from the list of servers available by default from the X-Chat | Server list menu or add some of our own to the list from the same menu.

Most IRC servers expect that we identify ourselves to the server. This is achieved by running the `identd` server on our machine. The `identd` server listens on port 113 for connections using the `ident` protocol and processes requests from remote machines asking for the identity of the user attempting to connect to the remote machine. `identd` is available as an RPM that should be installed separately as it is not part of the default installation. Chapter 4 has information on using the package manager for installing RPMs.


## Printmail reader

Although printmail isn't strictly a mail reader, it can be used as a part of managing your mail messages. The printmail command formats the mail in any file you give it (either your default mailbox or a saved mail message file) and formats the mail in a nicer form for printing. A command such as `printmail | lpr` will format the contents of your mailbox and output it to the printer (printmail assumes plain-text files, so don't use this with HTML messages or you will see a lot of junk).

## Incoming mail checkers

There are a couple of commands that aren't e-mail readers or composers. However, these programs let you quickly check whether you have any messages in your mailbox. The following are two such programs:

- **messages** — Does a quick count of the messages in your mailbox.
- **newmail** — Monitors mailboxes at intervals you choose (every so many seconds) and sends a message to your Terminal window when new mail arrives.

## Participating in Newsgroups

Usenet news is another feature that has been around almost as long as the Internet. Using a newsreader, and even many regular mail readers, you can select from literally thousands of topics and participate in discussions on those topics. To participate, you simply read the messages people have posted to the group, respond to those that you have something to say about, and send your own messages to start a discussion yourself.

To get started, you basically need a newsreader and access to a news server computer. As with e-mail, Mozilla uses Mozilla Mail and Netscape Navigator uses the Messenger mail program to let you participate in newsgroups. Traditional UNIX-style newsreaders include *trn* and *tin*, which are full-screen, text-based newsreaders.

> **TIP:** If you have never used a newsgroup before, check out the `news.announce.newusers` newsgroup. It's there to answer questions from new users.

## Netscape Messenger for newsgroups

Before you can begin using news groups you need to identify the news server you are using, identify yourself, and choose the newsgroups you want to access.

### Connecting to the news server

To begin using newsgroups, you need to open the Netscape Preferences window and add the news server's name and port number as follows:

1. From the Messenger window, choose **Edit → Preferences** to bring up the Netscape Preferences window.
2. In the Netscape Preferences window, click the down-arrow next to **Mail & Newsgroups**, then select **Newsgroups Servers**.
3. On the Newsgroup and Server page that appears, click **Add**. A pop-up window appears.
4. Type the name of your news server and, if necessary, the port number for news on that server. (The default news port is 119. You can obtain the name of the news server from your ISP or your system administrator at work. By convention, the name often has "news" or "nw" at the beginning.)
5. You can select to use encrypted (Secure Socket Layer) connections or to always use a name and password with the connection to your news server.
6. Click **OK** to accept the news server entry.
7. Other selections on the Newsgroups Servers page let you select a server and set it as the default or prompt you if there are more than a certain number of newsgroup messages downloaded to you (500 by default). Finally, you can choose which directory to use to hold your newsgroup messages (your home directory is used by default).
8. Click **OK**.

If your news server was properly identified and your connection to that server is working, you can open the Netscape Messenger window to begin participation in newsgroups. Connection to the news server occurs when you select news in the Messenger window. You must have a Netscape Messenger mail account configured to post messages to a newsgroups.

### Using newsgroups

To participate in newsgroups, you need to choose the ones that interest you from a list of available newsgroups. Before you start configuring your newsgroups, you should create a valid mail account through Netscape Messenger (so you can fully participate once you begin using newsgroups). You can then subscribe to your favorite newsgroups so that they are available every time you use Netscape Messenger.

### Subscribing to newsgroups

The following procedure describes how to subscribe to a newsgroup in Netscape Messenger.

1. Open Netscape Messenger (**Communicator → Messenger** from the Netscape window).
2. Right-click on the news server name in the left column.
3. In the menu that appears, click **Subscribe to Newsgroups**. A newsgroup subscription window appears, as shown in Figure 9-9.

![](img/1744bde8c889adfab3fc911e1687fecf_367_0.png)

Figure 9-9: Choose from thousands of newsgroups in the newsgroup subscription window in Netscape Messenger.

What appears (after a few minutes or more) in the subscription list are top-level newsgroup names. Newsgroups are organized in a hierarchy, similar to Internet domain names — levels are separated by dots (although newsgroup names start at the left and go down to the right).

4. Click the plus sign next to a category to see which groups in that category interest you.
5. When you see a newsgroup that interests you, click it and select **Subscribe**.
6. Click **OK**. The subscribed newsgroup appears in your Messenger window under the name of the news server.
7. Click the newsgroup in Messenger. Recent messages from that newsgroup are downloaded to your Messenger window.

## Reading newsgroup messages

Reading newsgroup messages is similar to reading mail messages. You simply click on a message that interests you or move to it using the up and down arrow keys. The message will appear in the message pane in the lower-right corner of the Messenger window.

The concept of threads should be mentioned here: When someone posts a message to a newsgroup, usually one or more people respond to it. Because it is useful to read messages and responses together, these messages are grouped together in threads. A plus (+) next to a message indicates that there are responses to that message. Click the plus to see the available threads. Threads make it easy to see a group of messages on a topic that interests you or to skip over a topic that doesn't.

## The Pan newsreader

> **NOTE:** To use pan you need to install the pan RPM package from CD-2 of the Red Hat Linux distribution that comes with this book. For further information about pan, refer to the following Web site: `http://pan.rebelbase.com`. An rpm package is probably available.

The Pan newsreader is a graphical application for reading, managing, and interacting with newsgroups. It is particularly adept at displaying attached pictures and downloading binaries. The interface is very intuitive and easy to use.

Pan is designed for the Gnome desktop. If you are running another desktop environment, however, you can still use Pan as long as you have the gnome-libs software package installed. After that, Pan works on KDE, Window Maker, or other desktop environments.

To open the Pan newsreader from the Gnome desktop menu, choose **Programs → Internet → Pan**. The first time you start Pan, the Pan wizard runs to allow you to configure the newsreader. Have your e-mail address and your news server’s name ready. When the wizard is done, you can download the list of newsgroups available from your news server.

## Participating in AOL Instant Messaging with Gaim

Gaim is an AOL Instant Messaging client program that runs in Linux. Because it is based on AOL’s Open IM architecture (`http://aim.aol.com/openim`), it has the same messaging features you get from AOL’s own messaging application.

To start Gaim from a Gnome desktop menu, choose **Programs → Internet → Gaim**. Figure 9-10 contains an example of the Gaim window:

![](img/1744bde8c889adfab3fc911e1687fecf_368_0.png)

Figure 9-10: Access your AOL Instant Messaging using GAIM.

From the main Gaim window, you have the following options:

- **Quit** — Exit from Gaim.
- **Accounts** — Add screen names, passwords, and options associated with your AOL Instant Messaging accounts.
- **Signon** — Sign on to AOL Instant Messaging by using your selected screen name.
- **About** — Displays information about GAIM and its creators.
- **Options** — Set options associated with AOL Instant Messaging and Chat windows.
- **Plug-ins** — Load plug-ins that can perform special functions, such as spell checking and auto-reconnection.

Besides AOL IM protocols, Gaim supports other messaging protocols, including instant messaging protocols from Yahoo!, the Microsoft Network, ICQ, and IRC.

## Using Remote Login, Copy, and Execution

This section describes some features for allowing users to use resources across a network. They are the *telnet*, *ssh*, *ftp*, *wget*, *rsync*, *rlogin*, *rcp*, and *rsh* commands.

> **CROSS-REFERENCE:** Because using these commands can represent significant security risks, Red Hat Linux is not configured to allow any of these commands to connect to it by default. For information on how to turn on these services on a Red Hat Linux server, refer to Chapter 14 (Computer Security Issues) and Appendix C (Running Network Services).

There is a nice set of commands available with Red Hat Linux for moving information between computers on a network — particularly between trusted computers. Two of the commands described in this section that are generally available are remote login and file transfer programs: *telnet* and *ftp*, respectively. Other commands for accessing FTP servers are *ncftp* and *gFTP*.

Two newer commands for copying files over the network are *wget* and *rsync*. Both of these tools can be used for efficiently downloading files that you can identify on the network.

Other commands described in this section are more specific to Red Hat Linux and other UNIX systems, but provide simplified ways of copying files, logging in, and executing commands among trusted systems: *rcp*, *rlogin*, and *rsh*, respectively. Also, a more secure tool for remote login called *ssh* has recently been added to the Red Hat Linux distribution. The *ssh* command can be used for remote execution as well.

### Using telnet for remote login

*Telnet* is a service provided by many different types of computer systems to enable remote users to log in to their machines over TCP/IP networks. The *telnet* command is the client

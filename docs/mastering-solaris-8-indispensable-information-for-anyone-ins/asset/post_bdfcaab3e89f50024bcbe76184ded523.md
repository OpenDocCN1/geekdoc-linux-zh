
to you and is not a copy. The code N means that the message is new. Code D means that the message has been marked for deletion.

If the message is from another user on your network, you could use the following commands:

- R to reply
- F to forward the message to someone else
- S to save the message in a message folder
- D to mark the message for deletion

There are two steps to deleting a message. First, you mark the message for deletion, and then you enter Y and the message is deleted. You can delete messages at any time, and you will be queried when you quit pine about whether you want the messages marked for deletion to be deleted at that time.

If you are already in the mailer and want to read the messages in the default folder (INBOX), you can select the Folder Index option from the main menu and bypass the folder list on the screen. This is a time-saver when you want to read just the messages in your INBOX and not have to access all the folders on the list. There is also a convenient shortcut to enter the Folder Index screen from the command line:

```
$ pine -i
```

Again, you can send mail such as a memo to more than one person at a time. You can access the message composer directly by typing the following command at the shell prompt (this will send messages to all three users):

```
$ pine al dave jim
```

You will be able to send messages to users on other systems if your system is a part of a network. You need to know their login name and a machine name and type both separated by the @ character, such as in the following example:

```
$ pine barrie@reliable
```

To send a message over the Internet, you would also have to know the domain name but not necessarily the machine name, such as in this example:

```
$ pine barrie@sosinsky-group
```

# The pine Newsreader

There is also a news interface called pine, which is related to the pine mail interface. There is consistency between commands, screen displays, and folder organization, which makes the newsreader easy to use. If you use the Netscape browser, you can use Netscape News as well. However, you have the option of using pine as a newsreader. You must have access to Usenet news for pine to function as a newsreader. If your site has no news server, you will not be able to read the news, so you should request a server from the system administrator.

If pine is installed on your system, you can start it as a newsreader by following these steps:

1. Enter pine at the command line to start pine.
2. Select Setup from the Main menu and wait until pine prompts you for the setup task on the bottom lines.
3. Enter C (Config) to ask pine to display the Setup Configuration screen.
4. View and modify any aspects of the configuration you wish to change.
5. Highlight the pine variable nntp-server and select A if it’s not already set.
6. Enter the name of the news server.

This is usually all you need to do to start pine as a newsreader. Each time you run pine, it will automatically contact the news server as you enter commands to read and post the news. If you are already accustomed to seeing the Folder List screen containing the INBOX and sent-mail and saved-messages folders, you will be familiar with the way pine displays individual folders within a collection when you select Folder List. Once the news is enabled, an additional collection called, appropriately, the news-collection is automatically defined, and the Folder List screen changes to display a list of the two folder collections (mail and news) instead. You will see a name identifying each collection. Highlight the line that says Select Here to See Expanded List. This will make the corresponding collection current. Highlight the line for the news-collection to let pine know that you plan to use the news feature. The command lines at the bottom of the screen will show that the label for command D has changed from Delete to Unsubscribe and that the label for command A has changed from Add to Subscribe.

# Sharing Information

Information regarding Solaris 8 can be found in several ways. One of the most widely used services is Usenet.

Usenet is an informal information service somewhat like an electronic bulletin board that allows users with common interests to exchange information and news items. Usenet has been around since the early 1980s when the IT community decided to share information on topics of common interest. Information was passed along over dial-up telephone lines using Unix’s uucp utility. Because of its popularity, major changes in uucp were needed to handle the volume of messages and sites. Today, the news travels over network links using a sophisticated protocol specifically designed for this purpose. It is called Network News Transfer Protocol (NNTP). Messages are stored in a standard format and are read by one of many public domain programs available. One of the older interfaces is called readnews. You can use others such as rn and its X Window System release, xrn, to browse through the articles that are available and reply or create articles of your own. In addition to rn and xrn, popular interfaces are tin, nn, and xnews. You can also Read Usenet news in CDE by using the Netscape Message Center.

Usenet software has been ported to non-Unix systems, so the community of netnews users has grown considerably. Netscape includes as part of its Web browser a graphical interface called Netscape News that you can use to read news. As is the Unix tradition, categories of netnews groups are structured hierarchically. At the top level are designations such as comp, misc, rec, sci, soc, and talk. These abbreviations stand for computer, miscellaneous, recreational, science, social issues, and talk discussions, respectively.

There is usually one regional category at the top level that includes information about local events. New categories are always being added. Newsgroup names resemble domain names but are read from left to right like Solaris filenames. For example, talk.politics, soc.singles, rec.racing, and so on are just a few of the newsgroups.

Using Usenet requires patience and perseverance, but you will certainly get to what you need and meet some interesting people along the way. There are netnews archives where you can most likely find an answer to almost any question because others have probably had the same question at one time or another. You can read Usenet news to find out about new tools and services. The comp.os.Unix hierarchy is always of interest to Unix users. People will announce the availability of free software there and give instructions on how to get a copy for your own use.

There are some great resources for questions and answers about Solaris 8 on the World Wide Web. The comp.unix.solaris forum is a Usenet group for Solaris 8 information and discussion. It also allows you to contribute your knowledge to assist others who have questions. You may be able to provide them with an answer or two.

In addition to Usenet, there are other ways to find and share information about Solaris on the Internet. The Solaris 8 FAQ, which is maintained by Casper Dik, is a wonderful source of general information. The latest version is at www.win5.uva.nl/pub/solaris/solaris8/.

For Intel users, there is a forum site called alt.solaris.x86 which is informative and kind to the neophyte. No question is considered too unimportant to answer. Both the SPARC and Intel platforms have an available FAQ site, which can be accessed at www.sunhelp.org/faq/sunadm.html.

For the latest Solaris 2 FAQs including an HTML version and other interesting goodies, contact `ftp://ftp.win5.uva.nl/pub/solaris`.

Another option for asking questions and finding answers is to use mailing lists. The Sun Manager's List is a famous list and contains questions, answers, and summaries of previous queries. Just about all Solaris-related topics are covered. There is also an x86 mailing list that has great tips, tricks, and advice for those who are relatively new to Solaris 8. This is a good resource if you have difficulties with specific hardware configurations.

For more information about Solaris help resources, refer to Chapter 1, "The Solaris 8 Operating System."

# Apache

The Apache Project is a software development project that is managed jointly by a group of volunteers. Located all around the world, and using the Internet and the World Wide Web to communicate, this a core group that created a commercial, free source code implementation of an HTTP Web server with related documentation. Based on the NCSA httpd server, Apache is now a completely rewritten server with a good measure of security.

Solaris 8's distribution contains a version of the Apache Web server for you use. If you don't have the operating system's distribution or if you decide you need the latest version, the Apache Web server may be obtained free of charge from the Apache Group (`www.apache.org`). This will get you all the latest bug fixes and current security features. The prerelease of version 2 is now on the Internet for download for developers. One of the major reasons that Apache is free is that users often contribute by suggesting feature enhancements and bug fixes and by actively supporting others in public newsgroups. Individual effort is usually minimal, but the combination of everyone's input has resulted in a very strong product. Although users will still be using 1.3.20, it will not be long before version 2 is ready for the public. Version 2 has many new enhancements that make it even more robust.

If you decide to download Apache, be sure to do the following:

1. Obtain a valid IP address.
2. Obtain a host name to use for your Web server.
3. Have your Web server added to domain name server.
4. Use a separate machine as a Web server if you plan to support CGI or servlets.
5. Check your system to make sure it has required components for compiling Apache.


from other users on your Linux system or from remote mail accounts, will appear in your local inbox. Such a feature is helpful if you are using a mail client, such as Elm or Mail, that does not have the capability to access mail on your ISP’s mail server. You can implement such a feature with Fetchmail. Fetchmail checks for mail on remote mail servers and downloads it to your local inbox, where it appears as newly received mail (you will have to be connected to the Internet or the remote mail server’s network).

To use Fetchmail, you have to know a remote mail server’s Internet address and mail protocol. Most remote mail servers use the POP3 protocol, but others may use the IMAP, ESMTP, or POP2 protocols. Enter fetchmail on the command line with the mail server address and any needed options. The mail protocol is indicated with the -p option and the mail server type, usually POP3. If your e-mail username is different from your Linux login name, you use the -u option and the e-mail name. Once you execute the fetchmail command, you are prompted for a password. The syntax for the fetchmail command for a POP3 mail server follows:

```
fetchmail -p POP3 -u username mail-server
```

To use Fetchmail, connect to your ISP and then enter the fetchmail commands with the options and the POP server name on the command line. You will see messages telling you if mail is there and, if so, how many messages are being downloaded. You can then use a mail client to read the messages from your inbox. You can run Fetchmail in daemon mode to have it automatically check for mail. You have to include an option specifying the interval in seconds for checking mail.

```
fetchmail -d 1200
```

You can specify options such as the server type, username, and password in a .fetchmailrc file in your home directory. You can also have entries for other mail servers and accounts you may have. Instead of entering options directly into the .fetchmailrc file, you can use the fetchmailconf program. fetchmailconf provides a GUI interface for selecting Fetchmail options and entering mail account information. fetchmailconf runs only under X and requires that python and Tk be installed. It displays windows for adding news servers, configuring a mail server, and configuring a user account on a particular mail server. The expert version displays the same kind of windows, but with many more options.

Once it is configured, you can enter fetchmail with no arguments; it will read entries from your .fetchmailrc file. You can also make entries directly in the .fetchmailrc file. An entry in the .fetchmailrc file for a particular mail account consists of several fields and their values: poll, protocol, username, and password. Poll is used to specify the mail server name, and protocol, the type of protocol used. Notice you can also specify your password, instead of having to enter it each time Fetchmail accesses the mail server.

## Usenet News

Usenet is an open mail system on which users post messages that include news, discussions, and opinions. It operates like a mailbox that any user on your Linux system can read or send messages to. Users’ messages are incorporated into Usenet files, which are distributed to any system signed up to receive them. Each system that receives Usenet files is referred to as a site. Certain sites perform organizational and distribution operations for Usenet, receiving messages from other sites and organizing them into Usenet files, which are then broadcast to many other sites. Such sites are called backbone sites, and they operate like publishers, receiving articles and organizing them into different groups.

To access Usenet news, you need access to a news server. A news server receives the daily Usenet newsfeeds and makes them accessible to other systems. Your network may have a system that operates as a news server. If you are using an Internet service provider (ISP), a news server is probably maintained by your ISP for your use. To read Usenet articles, you use a newsreader—a client program that connects to a news server and accesses the articles. On the Internet and in TCP/IP networks, news servers communicate with newsreaders using the Network News Transfer Protocol (NNTP) and are often referred to as NNTP news servers. Or you could also create your own news server on your Linux system to run a local Usenet news service or to download and maintain the full set of Usenet articles. Several Linux programs, called news transport agents, can be used to create such a server. This chapter focuses on the variety of news readers available for the Linux platform. The configuration administration and architecture of the NNTP server are covered in Chapter 26.

Usenet files were originally designed to function like journals. Messages contained in the files are referred to as articles. A user could write an article, post it in Usenet, and have it immediately distributed to other systems around the world. Someone could then read the article on Usenet, instead of waiting for a journal publication. Usenet files themselves were organized as journal publications. Because journals are designed to address specific groups, Usenet files were organized according to groups called newsgroups. When a user posts an article, it is assigned to a specific newsgroup. If another user wants to read that article, he or she looks at the articles in that newsgroup. You can think of each newsgroup as a constantly updated magazine. For example, to read articles on the Linux operating system, you would access the Usenet newsgroup on Linux. Usenet files are also used as bulletin boards on which people carry on debates. Again, such files are classified into newsgroups, though their articles read more like conversations than journal articles. You can also create articles of your own, which you can then add to a newsgroup for others to read. Adding an article to a newsgroup is called posting the article.

> NOTE The Google Web site maintains online access to Usenet newsgroups. It has the added capability of letting you search extensive newsgroup archives. You can easily locate articles on similar topics that may reside in different newsgroups. Other sites such as Yahoo maintain their own groups that operate much like Usenet newsgroups, but with more supervision.

Linux has newsgroups on various topics. Some are for discussion, and others are sources of information about recent developments. On some, you can ask for help for specific problems. A selection of some of the popular Linux newsgroups is provided here:

| Newsgroup | Topic |
|---|---|
| comp.os.linux.announce | Announcements of Linux developments |
| comp.os.linux.admin | System administration questions |
| comp.os.linux.misc | Special questions and issues |


# 382 Linux Web Server Toolkit

![](img/e01f1106dd2902613fa07890c8baa7e6_409_0.png)

Figure 14-2: Mailto link causes the browser to open a window in which a user can compose an e-mail message.

## Accepting E-Mail

Once you use the preceding methods to get e-mail sent from your Web pages, you have to have a mail server running on your system to be able to accept and receive messages that come in.

OpenLinux Lite includes several e-mail servers. All are based on the Internet standard SMTP (Simple Mail Transport Protocol). The sendmail server is installed and running by default on your OpenLinux system. You can see that it is running by using this command:

```
ps -aux | grep sendmail
```

By default, the sendmail program accepts e-mail for any user on your system. For example, if you use the adduser command or the lisa administration program to create a new user named anne, e-mail will immediately be accepted for anne@servername.com.

All remains is to read the messages. If you have a graphical e-mail reader for Linux, like the Netscape Navigator Gold or Zmail, reading your e-mail is very easy. If you don't, you can use the elm mail reader program, which is installed by default on your OpenLinux Lite system. The elm program is a text-based mail reader. It includes onscreen instructions, but it can be challenging to become familiar. The first time you start elm, it creates two directories to hold your mail while you are reading it. You can start elm from any command line, including within the X Window System.

```
$elm
```

## Using Aliases

One feature of e-mail you may want to use immediately is to have several e-mail addresses that are routed to a user's e-mail account. For example, you can have an e-mail address called "info" or "sales," and have them both sent to your personal mailbox. Later, if you want to e-mail to another person's e-mail, you can simply alter how they are routed.

These are e-mail aliases. Basically, you're saying that "info" or "sales" is an alias to your e-mail address, though no one knows it. If you use aliases, you may want to turn off the EXPN directive in the sendmail configuration to prevent people from discovering your aliases.

To use an e-mail alias, just add a line to the /etc/aliases file, like this (a comment line is included to explain the purpose of the aliases):

```
# send all info inquiries to john for now
info: johnr
```

To make this alias effective, you must execute the newialases command while logged in as user root to process the /etc/aliases file with your changes in it.

```
$ newialases
```

Now if I send an e-mail message from anywhere to info@server1.com, it will show up in the mailbox of johnr. One alias can go to several actual users, and aliases all go to one user. An alias can also send e-mail messages directly to a file for archiving, or pipe a message to an external command for processing.

## Configuring E-Mail

Unfortunately, configuring the e-mail server in OpenLinux is completely beyond the scope of this book. The sendmail server can do an amazing variety of things, but configuring it is very challenging. If you need to provide anything more than the most basic e-mail service, follow these steps:

- 1. Review the contents of the /etc/sendmail.conf file.
- 2. Enter the command sendmail.

Get a copy of Sendmail, published by O'Reilly & Associates.

Consider using the popular q-mail server (included on the OpenLinux Lite CD-ROM) as an alternative to the old standby sendmail. q-mail provides excellent performance with fewer security issues than sendmail.

## Including Other Services

There are several other service protocols that are supported by most Web browsers, but they are not as widely used because the information they provide is, in most cases, readily available in a format like the Web (http) or FTP. These services are briefly mentioned here.

## Using Usenet Newsgroups

Newsgroups are like online discussion forums on about 12,000 topics, ranging from popular culture (and less popular, and cultured), to science and politics, to computers and everything in between. You may have heard of groups like alt.fans.friends, where everyone who's interested in the latest episode of their favorite TV show exchanges questions and comments. Newgroups are similar to an online chat room, where all posted comments (each one is called an article) are listed individually by e-mail messages, rather than onscreen in real time. You can include a URL with a link to a newsgroup by using a format like this:

You may also want to review posting in the <A HREF=news:soc.genealogy>Genealogy</A> newsgroup.

Notice that the format is different from other URL styles. There is no server mentioned per. The user's browser must know where a news server is and be able to collect and display the articles in the soc.genealogy newsgroup when that link is selected.

More and browsers are able to view newsgroups, but it's not a standard information that a source of Web pages use. After all, you can place the specific files you want to refer in your FTP archive; you know what someone will find in a newsgroup. It just gives them an avenue to explore possible connections to the topic on your Web page. Figure 14-3 shows a Web browser with a newsgroup window.

Of course, if you want to have your own news server, you can do that also. OpenLinux includes the software to set up a full news server using the standard NNTP protocol. You will need to locate a "newsfeed" where most of the articles come from. Been, however, that a full newsfeed may generate gigabytes of each day. In addition, I mention that the e-mail program was quite challenging to set up. A news server is substantially more difficult than that. You might consider pointing to your ISP as your news server, using Deja News in your Web browser (see http://www.dejanews.com), or looking for a commercial provider.

![](img/e01f1106dd2902613fa07890c8baa7e6_412_0.png)

Figure 14-3: Newsgroups can be viewed within some Web browsers, such as Netscape Navigator 3.0 for Linux.

You can read news articles using a command-line program like tin or tr, or a graphical program like Netscape Navigator for OpenLinux (which is not included with the CD-ROM in this book).

## Using Gopher

Before the Web was invented, a system called Gopher was very popular as a method of accessing UNIX systems across the Internet. Gopher provides an interface to a UNIX directory structure that includes many of the same features for generating a directory listing that a Web server now provides. For example, you can specify file types and associated icons, a header file to appear with a directory, and descriptions for each file to replace cryptic filenames. Figure 14-4 shows a Gopher display within a Web browser.

You can set a Gopher server using the free software that comes with OpenLinux from the University of Minnesota. Install the gn-2.22-1.i386.rpm package to use the Gopher server. You can see http://www.yahoo.com/Computers_and_Internet/Internet/Gopher for more references on Gopher.

![](img/e01f1106dd2902613fa07890c8baa7e6_413_0.png)

Figure 14-4: A Gopher site can be linked to and displayed within almost all browsers.

In addition, you may often find existing information on other Gopher sites that you want to link to your Web pages. All browsers support this format, using the following syntax for a link:

You can also review the <A HREF=gopher://gopher.utah.edu/>University of Utah Chemical Archives.</A>

If you're connected to the Internet, you can use the Veronica program to explore the contents of Gopher sites on the Internet.

## Using WAIS

WAIS is the Wide Area Information Service. It provides complete indexes of a server's contents for online subject searches using complex queries. WAIS capabilities are integrated into some browsers, but most still require a gateway on the Web to access and return WAIS search results.

As Gopher, WAIS has diminished in popularity with the advent of incredible searching and indexing tools for the entire Internet, such as AltaVista (http://www.altavista.digital.com), which indexes all Web sites, FTP sites, and newsgroup postings.


## The slrn News Client

The slrn program is a text-based newsreader program included with the Ubuntu distribution. It uses the ncurses package to paint text-based windows on the terminal screen. slrn can be used to both read and post articles to newsgroups on a configured news server. If you want to use the same newsreader on different platforms, slrn runs on Linux, Mac, OS2, BeOS, Windows, and VMX. It now provides true offline reading capabilities.

The slrn program is included in the slrn RPM package; you install it by using the yum or rpm command. After you have installed slrn, you need to create a local configuration file. Begin by setting an environment variable:

```
$ export NNTSERVER=news.andbhudson.co.uk
```

Of course, you will use your own news servers’ domain name.

Then create your local configuration file with

```
$ slrn -f .jnewsrc -- create
```

and launch slrn. The configuration file, located at /etc/slrn.rc, is a well-commented file that is easy to modify and customize.

When slrn starts, it displays a list of the groups available on the news server. You select the group you want to read articles from, and then select the individual articles. Figure 8.12 shows a slrn screen example.

![](img/e464b828c497c99e41f61d4c55f1c0db_203_0.png)

FIGURE 8.12 A slrn article display example showing a posted message about a FAQ for Internet mail

## The Pan News Client

Pan is a graphical newsreader client that works with GNOME and is the default newsreader for Ubuntu. If you have the GNOME libraries installed (and they usually are installed by default), you can also use Pan with the *K Desktop Environment (KDE)*. Pan can download and display all the newsgroups and display posted news articles. You can launch it by using the GNOME or KDE desktop panel or from the command line of an X terminal window with the command `pan &`. Pan supports combining multipart messages and the yenc encoding/decoding protocol. Figure 8.13 shows a sample Pan display. Unlike the slrn program, Pan does not require a systemwide default or user-defined NNTPSERVER environment variable to define the news server address, but you do need to configure Pan.

The first time you run Pan, a Configuration Wizard appears and prompts you for your name, the SMTP server name, the NNTP server name, and the name you want to use to identify the connection. (In the example shown in Figure 8.14, we use Plus Net.) After the wizard is finished, you are prompted to download a list of the newsgroups the server provides; this might take a while. If you need to change the news server or add an additional server, you can access the Preferences item under the Edit menu to bring up the list of servers. Then you highlight the appropriate one and click Edit to change it or just click the New button to add a new news server.

![](img/e464b828c497c99e41f61d4c55f1c0db_204_0.png)

**FIGURE 8.13**  The Pan graphical newsreader is one of the nicest available for Linux, shown here browsing the alt.comp.os.linux newsgroup.

![](img/e464b828c497c99e41f61d4c55f1c0db_205_0.png)

FIGURE 8.14 The Pan news server configuration window.

## The Thunderbird News Client

Along with Firefox, the Thunderbird mail and news client is a direct descendant of the Mozilla suite. Designed to be lightweight and with a clean interface, Thunderbird does many of the things that the Mozilla news client can do but is a separate application from Firefox.

To add a new account to Thunderbird, click Tools, Account Settings, and select Add Account. Select the news account and follow the prompts giving Thunderbird all the information it needs.

When you have finished providing Thunderbird with all the relevant information, click OK, and you arrive at Thunderbird's default view. Along the left pane you will see the new news server account. Click it and then select Manage Newsgroup Subscriptions.

## Internet Relay Chat

As documented in RFC 2812 and RFC 2813, the IRC protocol is used for text conferencing. Like mail and news, IRC uses a client/server model. Although it is rare for an individual to establish an IRC server, it can be done. Most people use public IRC servers and access them with IRC clients.

Ubuntu provides a number of graphical IRC clients, including X-Chat, licq-kde, and Mozilla-chat, but there is no default chat client for Ubuntu. Ubuntu also provides the

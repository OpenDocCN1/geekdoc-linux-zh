
## NOTE

The format of newsgroup articles follows the strict guidelines defined in the Internet standards document Request For Comments (RFC) 1036. Each article must contain two distinct parts: header lines and a message body.

The header lines identify information about when and by whom the article was posted. The body of the message should contain only standard ASCII text characters. No binary characters or files should be posted within news articles. To get around this restriction, binary files are converted to text data, through use of either the standard UNIX uuencode program or the newer Multipurpose Internet Mail Extensions (MIME) protocol. The resulting text file is then posted to the newsgroup. Newsgroup readers can then decode the posted text file back into its original binary form.

A collection of articles posted in response to a common topic is called a *thread*. A thread can contain many articles as users post messages in response to other posted messages. Some newsreader programs allow users to track articles based on the threads to which they belong. This helps simplify the organization of articles in the newsgroup.

## TIP

The free news server news.gmane.org makes the Red Hat and Fedora mail lists available via newsgroups. It is a handy way to read threaded discussions and easier than using the Fedora mail list archives.

The protocol used to transfer newsgroup articles from one host to another is *Network News Transfer Protocol* (NNTP), defined in RFC 975. (You can search RFCs at ftp://metalab.unc.edu/pub/docs/rfc/; look at the file `rfc-index.txt`.) NNTP was designed as a simple client/server protocol that enables two hosts to exchange newsgroup articles in an efficient manner.

### The Pan News Client Newsreader

Whether or not your Fedora server is set up as a news server, you can use a newsreader program to read newsgroup articles. The newsreader programs require just a connection to a news server. It does not matter whether the news server is on the same machine or is a remote news server on the other side of the world.

Several programs are available for UNIX systems to connect to news servers to read and post articles in newsgroups. Here we discuss the Pan news client.

Pan is a graphical newsreader client that works with GNOME and is the default newsreader for Fedora. If you have the GNOME libraries installed (and they usually are installed by default), you can also use Pan with the *K Desktop Environment* (KDE). Pan can download and display all the newsgroups and display posted news articles. You can launch it by using the GNOME or KDE desktop panel or from the command line of an X terminal window with the command pan &. Pan supports combining multipart messages and the yenc encoding/decoding protocol. Figure 5.15 shows a sample Pan display.

![](img/34e72348d53ca54c2a1d9c871316691b_150_0.png)

FIGURE 5.15 The Pan graphical newsreader is one of the nicest available for Linux, shown here browsing through a Red Hat usergroup.

The first time you run Pan, a configuration wizard appears and prompts you for your name, the SMTP server name, the NNTP server name, and the name you want to use to identify the connection. (In the example shown in Figure 5.16, we use a custom news server.) After the wizard has finished, you are prompted to download a list of the newsgroups the server provides; this might take a while. If you need to change the news servers or add an additional server, you can access the Preferences item under the Edit menu to bring up the list of servers. Then, you highlight the appropriate one and click Edit to change it or just click the New button to add a new news server.

![](img/34e72348d53ca54c2a1d9c871316691b_151_0.png)

FIGURE 5.16 The Pan news server configuration window.

### Videoconferencing with Ekiga

Ekiga is an Internet videoconferencing application that provides two-way voice and picture transmission over the Internet by using the H.323 protocol for IP telephony (also known as *Voice over IP [VoIP]*). It is an application similar to Microsoft NetMeeting and is provided with Fedora as the default videoconferencing client.

Before you can take full advantage of the phone and videoconferencing capabilities of Ekiga, you must configure a full-duplex-capable sound card and video device (see Chapter 7, "Multimedia") and a camera.

Ekiga is found in the Internet menu as *Videoconferencing*; you click the icon to launch it. When you start the Ekiga application for the first time, a configuration wizard (called a *druid*) runs and you are greeted by the first of four configuration screens. You simply enter your name, email address, and location and select your connection type. The settings for your audio and video devices are automatically detected; you can view them by selecting the Preferences item from the Edit menu. Figure 5.17 shows Ekiga in action, ready to dial another user.

When you have Ekiga running, you must register (from within Ekiga) with the server at http://ekiga.net/ to enable conferencing; Ekiga does this automatically for you if you told it to do so during the initial configuration.

You can find an informative FAQ at the Ekiga home page at http://www.Ekiga.org/ that you should read in full before using Ekiga. Also, an excellent article about VoIP is at http://freshmeat.net/articles/view/430/.

![](img/34e72348d53ca54c2a1d9c871316691b_152_0.png)

FIGURE 5.17 Ekiga is surprisingly simple to use. A video source is not necessary; a static picture can be used, too.

## NOTE

If you frequently use VoIP applications such as Ekiga, you will tire of repetitively typing in long IP addresses to make connections. To avoid this hassle, you can use a gate-keeper—similar in purpose to a DNS server—to translate names into IP addresses. OpenH323 Gatekeeper is one such popular gatekeeper application. It is not provided with Fedora, but you can obtain it from http://www.gnugk.org/.

## Reference

-   ▶ http://www.novell.com/—The home of Ximian Evolution, the standard email client for Fedora.
-   ▶ http://www.mozilla.org/—The home page for Mozilla Firefox, Thunderbird, and the Mozilla Suite.
-   ▶ http://www.spreadfirefox.com/—The Firefox advocacy home page is useful for converting those Internet Explorer types.
-   ▶ http://ekiga.net/—Sign up here for a free SIP account for use with Ekiga.

### CHAPTER 6 Productivity Applications

#### IN THIS CHAPTER

-   What Is In OpenOffice.org?
-   Office Suites for Fedora
-   Productivity Applications Written for Microsoft Windows
-   Reference

With the rapid growth of open source software, businesses have directly benefited from developments in office productivity suites. Many businesses already use OpenOffice.org and its commercial counterpart, StarOffice, and they are already enjoying the cost benefits of not having to pay license fees or support costs. Of course, more suites are available than just OpenOffice.org, and in this chapter we explore the options available.

## NOTE

> OpenOffice.org is not 100% compatible with Microsoft Office. Why is this? Well, Microsoft is notoriously secretive about its proprietary file formats, and the only way that OpenOffice.org could ensure compatibility would be to reverse-engineer each file format, an exercise akin to taking apart a telephone to see how it works. This reverse-engineering could be classed as illegal under U.S. law, which would make OpenOffice.org somewhat of a potential hot potato if they chose this path. However, OpenOffice.org manages to maintain a very high standard of importing and exporting, so you should not experience too many problems.

A productivity suite could be classed as containing two or more applications that could be used for creating documents, presentations, spreadsheets, and databases. Other applications could include email clients, calculators/formula editors, and even illustration packages. Commonly they are all tied together by a default look and feel, which makes sticking to one particular suite much easier. Because Fedora uses OpenOffice.org as its standard office suite, we

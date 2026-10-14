
Usenet newsgroups act as a form of public bulletin board system. Any user can subscribe to individual newsgroups and send (or post) messages (called articles) to the newsgroup so that all the other subscribers of the newsgroup can read them. Some newsgroups include an administrator, who must approve each message before it is posted. These are called moderated newsgroups. Other newsgroups are open, allowing any subscribed member to post a message. When an article is posted to the newsgroup, it is transferred to all the other hosts in the news network.

Usenet newsgroups are divided into a hierarchy to make it easier to find individual newsgroups. The hierarchy levels are based on topics, such as computers, science, recreation, and social issues. Each newsgroup is named as a subset of the higher-level topic. For example, the newsgroup comp relates to all computer topics. The newsgroup comp.laptops relates to laptop computer issues. Often the hierarchy goes several layers deep. For example, the newsgroup comp.databases.oracle.server relates to Oracle server database issues.

## NOTE

The format of newsgroup articles follows the strict guidelines defined in the Internet standards document Request for Comments (RFC) 1036. Each article must contain two distinct parts: header lines and a message body.
The header lines identify information about when and by whom the article was posted.
The body of the message should contain only standard ASCII text characters. No binary characters or files should be posted within news articles. To get around this restriction, binary files are converted to text data, through use of either the standard Unix uuencode program or the newer Multipurpose Internet Mail Extensions (MIME) protocol. The resulting text file is then posted to the newsgroup. Newsgroup readers can then decode the posted text file back into its original binary form.

A collection of articles posted in response to a common topic is called a thread. A thread can contain many articles as users post messages in response to other posted messages. Some newsreader programs allow the user to track articles based on the threads to which they belong. This helps simplify the organization of articles in the newsgroup.

## TIP

The free news server news.gmane.org makes the Red Hat and Ubuntu mail lists available via newsgroups. The beta list is available as gmane.linux.redhat.rh1.beta. It is a handy way to read threaded discussions and easier than using the Ubuntu mail list archives.

The protocol used to transfer newsgroup articles from one host to another is Network News Transfer Protocol (NNTP), defined in RFC 975. (You can search RFCs at ftp://metalab.unc.edu/pub/docs/rfc/; look at the file rfc-index.txt.) NNTP was designed as a simple client/server protocol that enables two hosts to exchange newsgroup articles in an efficient manner.

The first time you run Pan, a configuration wizard appears and prompts you for your name, the SMTP server name, the NNTP server name, and the name you want to use to identify the connection (in the example shown in Figure 5.15, we use a custom news server). After the wizard is finished, you are prompted to download a list of the news-groups the server provides; this might take a while. If you need to change the news server or add an additional server, you can access the Preferences item under the Edit menu to bring up the list of servers. Then, you highlight the appropriate one and click Edit to change it or just click the New button to add a new news server.

![](img/7aaa8e4f2209bf9f2fb443905096e94c_148_0.png)

FIGURE 5.15 The Pan news server configuration window.

## Videoconferencing with Ekiga

Ekiga is an Internet videoconferencing application that provides two-way voice and picture transmission over the Internet by using the H.323 protocol for IP telephony (also known as Voice over IP [VoIP]). It is an application similar to Microsoft NetMeeting and is provided with Ubuntu as the default videoconferencing client.

Before you can take full advantage of the phone and videoconferencing capabilities of Ekiga, you must configure a full-duplex-capable sound card and video device (see Chapter 7, “Multimedia Applications”) as well as a camera.

Ekiga is found in the Internet menu as Videoconferencing; you click on the icon to launch it. When you start the Ekiga application for the first time, a configuration wizard

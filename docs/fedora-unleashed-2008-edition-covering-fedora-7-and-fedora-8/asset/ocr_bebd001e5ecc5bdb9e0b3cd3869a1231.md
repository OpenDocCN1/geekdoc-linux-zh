# NOTE

The format of newsgroup articles follows the strict guidelines defined in the Internet standards document Request For Comments (RFC) 1036. Each article must contain two distinct parts: header lines and a message body.

The header lines identify information about when and by whom the article was posted. The body of the message should contain only standard ASCII text characters. No binary characters or files should be posted within news articles. To get around this restriction, binary files are converted to text data, through use of either the standard UNIX uuencode program or the newer Multipurpose Internet Mail Extensions (MIME) protocol. The resulting text file is then posted to the newsgroup. Newsgroup readers can then decode the posted text file back into its original binary form.

A collection of articles posted in response to a common topic is called a *thread*. A thread can contain many articles as users post messages in response to other posted messages. Some newsreader programs allow users to track articles based on the threads to which they belong. This helps simplify the organization of articles in the newsgroup.

# TIP

The free news server news.gmane.org makes the Red Hat and Fedora mail lists available via newsgroups. It is a handy way to read threaded discussions and easier than using the Fedora mail list archives.

The protocol used to transfer newsgroup articles from one host to another is *Network News Transfer Protocol* (NNTP), defined in RFC 975. (You can search RFCs at ftp://metalab.unc.edu/pub/docs/rfc/; look at the file `rfc-index.txt`.) NNTP was designed as a simple client/server protocol that enables two hosts to exchange newsgroup articles in an efficient manner.

# The Pan News Client Newsreader

Whether or not your Fedora server is set up as a news server, you can use a newsreader program to read newsgroup articles. The newsreader programs require just a connection to a news server. It does not matter whether the news server is on the same machine or is a remote news server on the other side of the world.

Several programs are available for UNIX systems to connect to news servers to read and post articles in newsgroups. Here we discuss the Pan news client.

Pan is a graphical newsreader client that works with GNOME and is the default newsreader for Fedora. If you have the GNOME libraries installed (and they usually are installed by default), you can also use Pan with the *K Desktop Environment* (KDE). Pan can
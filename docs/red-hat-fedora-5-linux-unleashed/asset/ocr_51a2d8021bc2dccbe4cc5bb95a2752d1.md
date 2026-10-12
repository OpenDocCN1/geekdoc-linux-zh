# Newsgroups

Usenet newsgroups act as a form of public bulletin board system. Any user can subscribe to individual newsgroups and send (or *post*) messages (called *articles*) to the newsgroup so that all the other subscribers of the newsgroup can read them. Some newsgroups include an administrator, who must approve each message before it is posted. These are called *moderated* newsgroups. Other newsgroups are *open*, allowing any subscribed member to post a message. When an article is posted to the newsgroup, it is transferred to all the other hosts in the news network.

Usenet newsgroups are divided into a hierarchy to make it easier to find individual newsgroups. The hierarchy levels are based on topics, such as computers, science, recreation, and social issues. Each newsgroup is named as a subset of the higher-level topic. For example, the newsgroup `comp` relates to all computer topics. The newsgroup `comp.laptops` relates to laptop computer issues. Often the hierarchy goes several layers deep. For example, the newsgroup `comp.databases.oracle.server` relates to Oracle server database issues.

> **NOTE**
> 
> The format of newsgroup articles follows the strict guidelines defined in the Internet standards document Request for Comments (RFC) 1036. Each article must contain two distinct parts: header lines and a message body.
> 
> The header lines identify information about when and from whom the article was posted. The body of the message should contain only standard ASCII text characters. No binary characters or files should be posted within news articles. To get around this restriction, binary files are converted to text data by using either the standard UNIX uuencode program or the newer Multipurpose Internet Mail Extensions (MIME) protocol. The resulting text file is then posted to the newsgroup. Newsgroup readers can then decode the posted text file back into its original binary form.

A collection of articles posted in response to a common topic is called a *thread*. A thread can contain many articles as users post messages in response to other posted messages. Some newsreader programs allow the user to track articles based on the threads they belong to. This helps simplify the organization of articles in the newsgroup.

> **TIP**
> 
> The free news server `news.gmane.org` makes the Red Hat and Fedora mail lists available via newsgroups. The beta list is available as `gmane.linux.redhat.rhl.beta`. It is a handy way to read threaded discussions and easier than using the Fedora mail list archives.

The protocol used to transfer newsgroup articles from one host to another is Network News Transfer Protocol (NNTP), defined in RFC 977. (You can search RFCs at `ftp://metalab.unc.edu/pub/docs/rfc/`; look at the file `rfc-index.txt`.) NNTP was designed as a simple client/server protocol that enables two hosts to exchange newsgroup articles in an efficient manner.
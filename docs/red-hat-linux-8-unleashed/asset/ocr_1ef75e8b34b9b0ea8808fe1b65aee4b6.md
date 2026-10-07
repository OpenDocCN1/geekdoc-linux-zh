# An Overview of Network News

A collection of articles posted in response to a common topic is called a thread. A thread can contain many different articles as users post messages in response to other posted messages. Some newsreader programs allow the user to track articles based on the threads they belong to. This simplifies the organization of articles in the newsgroup.

The protocol used to transfer news articles from one host to another is Network News Transfer Protocol (NNTP), defined in RFC 977. (You can search RFCs at http://www.ietf.org/frc/html.html) NNTP was designed as a simple client/server protocol that allows two hosts to exchange newsgroup articles in an efficient manner.

# Types of News Servers

Unless you are an Internet service provider (ISP) or are planning to provide news services to a large group of people, you will likely not be setting up or administering a news server for your own use. If this is the case, you can skip ahead to the section "Configuring a Local News Server."

You can use a number of different methods to implement a news server on a network, and the way you intend to use the news server determines how you must configure it. The following sections describe three of the most popular types of news servers on local networks: full newsfeed servers, leaf node servers, and local news servers.

# Full Newsfeed Servers

A full newsfeed server receives all the Usenet newsgroup postings from upstream news server (a large, commercial server). Because it receives all the newsgroups, it can serve as an upstream news server for other sites, providing newsfeeds to other servers. The servers themselves might or not subscribe to all the newsgroups. Besides providing newsfeeds for other sites, the full newsfeed server can also support newsreader clients that connect to the news server to read and post articles to newsgroups.

Each news server receives newsfeeds and forwards postings to one or more remote news servers. The full newsfeed server must have enough storage capacity to maintain the newsfeeds for all the newsgroups it. If the remote news servers don't connect to download their newsfeeds on a daily basis, the newsfeed server must be able to maintain all the newsfeeds for the intervening days. This can require a very large amount of data storage capacity, beyond the capabilities of systems that are common among home users and businesses.

# Leaf Node Servers

A leaf node server receives newsfeeds only from upstream news servers: It doesn't have other news servers. This is the most common configuration for corporate news servers. Because the leaf node server doesn't have to feed other news servers, it doesn't have to retrieve all the newsgroups from its upstream newsfeed. You can pick and choose which newsgroups the news server retrieves from the newsfeed. The main role of the leaf node news server is to provide news service to newsreader clients.
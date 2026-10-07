
# An Overview of Network News

A collection of articles posted in response to a common topic is called a thread. A thread can contain many different articles as users post messages in response to other posted messages. Some newsreader programs allow the user to track articles based on the threads they belong to. This simplifies the organization of articles in the newsgroup.

The protocol used to transfer news articles from one host to another is Network News Transfer Protocol (NNTP), defined in RFC 977. (You can search RFCs at http://www.ietf.org/rfc/html.html) NNTP was designed as a simple client/server protocol that allows two hosts to exchange newsgroup articles in an efficient manner.

# Types of News Servers

Unless you are an Internet service provider (ISP) or are planning to provide news services to a large group of people, you will likely not be setting up or administering a news server for your own use. If this is the case, you can skip ahead to the section "Configuring a Local News Server."

You can use a number of different methods to implement a news server on a network, and the way you intend to use the news server determines how you must configure it. The following sections describe three of the most popular types of news servers on local networks: full newsfeed servers, leaf node servers, and local news servers.

# Full Newsfeed Servers

A full newsfeed server receives all the Usenet newsgroup postings from upstream news server (a large, commercial server). Because it receives all the newsgroups, it can serve as an upstream news server for other sites, providing newsfeeds to other servers. The servers themselves might or not subscribe to all the newsgroups. Besides providing newsfeeds for other sites, the full newsfeed server can also support newsreader clients that connect to the news server to read and post articles to newsgroups.

Each news server receives newsfeeds and forwards postings to one or more remote news servers. The full newsfeed server must have enough storage capacity to maintain the newsfeeds for all the newsgroups it receives. If the remote news servers don't connect to download their newsfeeds on a daily basis, the newsfeed server must be able to maintain all the newsfeeds for the intervening days. This can require a very large amount of data storage capacity, beyond the capabilities of systems that are common among home users and businesses.

# Leaf Node Servers

A leaf node server receives newsfeeds only from upstream news servers: It doesn't have other news servers. This is the most common configuration for corporate news servers. Because the leaf node server doesn't have to feed other news servers, it doesn't have to retrieve all the newsgroups from its upstream newsfeed. You can pick and choose which newsgroups the news server retrieves from the newsfeed. The main role of the leaf node news server is to provide news service to newsreader clients.

# CHAPTER 20 News and Other Collaborative Communication

The leaf node does, however, have maintain a system for users to connect to the news server to read and post messages. This is often done by using UNIX, Microsoft Windows, or Apple Macintosh workstation software. Each client must connect to the leaf node to download articles from specific newsgroups, and it must upload postings made to the newsgroups. The leaf node must be able to forward new postings from customers to the newsfeed server.

# Local News Servers

An organization may not want to participate in the worldwide Usenet newsgroups but might want to use Usenet software to create its own news server to handle internal communications within the organization. Usually these communications need to remain private to the organization and don't need to be sent to all the Usenet hosts around the world. This is likely the most common use of a news server you might be asked to configure.

Two methods are used to implement a local news server. An organization may create a standalone news server that doesn't receive any newsfeeds from Usenet servers. The server contains only local newsgroups that are used for internal corporate communications. Alternatively, you can create on a Usenet server local newsgroups that aren't forwarded through any newsfeeds in the Usenet system. This allows organizations to create their own local newsgroups that their employees can participate in sharing their information with the rest of the world.

Thus, local newsgroups can be created on news servers that aren't connected to the Usenet network or that do not forward the local groups to their upstream newsfeeds. Any postings to the local newsgroups appear only on the local news server. The Usenet news servers allow clients to post articles to both the local and Usenet newsgroups. However, only articles posted to Usenet newsgroups are forwarded to the upstream news server. The local articles remain only on the local news server.

# Configuring a Local News Server

The InternetNews (INN) package is the most popular server software used on UNIX. The following sections describe how the package works, how to install it, and how to configure it as a local server. The information you'll learn here will help you avoid some of the common pitfalls while configuring your news server.

# The INN Package and Configuration Files

The INN package (which is formed around the innd daemon) contains many different executable programs and configuration files that allow the Red Linux server to work. Table 20.1 describes some of the INN programs included in the distribution.

| Program File | Description |
| :--- | :--- |
| ctlinnd | Allows the user to manually send control messages to the innd. |
| getlist | Obtains a list of newsgroups from a news server. |
| geophysics | Queries the database files for a specific message ID and returns the record information. |
| incheck | Examines INN configuration files and databases. |
| inval | Prints the values of parameters that are specified in. |
| innd | Handles all incoming feeds and spawns INN programs as needed. |
| instart | Starts the innd from the news user. |
| inreport | Summarizes INN logs into readable reports. |
| instat | Prints a snapshot of the current status of the INN system. |
| inwatch | Monitors the running INN system and, if necessary, throttles the feeds to help reduce load on the server. |
| mailpost | Manually sends a mail message into a specified newsgroup. |
| maked | Creates binary indexed database files from the history file. |
| make | Creates a history file of message IDs seen by the news server. |
| news.daily | Runs as a cron job to perform daily maintenance of the news server. |
| nnprd | Communicates with newsreaders via the innd daemon. |
| nptget | Connects to a remote news server and retrieves articles that are specified on the standard input. |
| nntsend | Connects to a remote news server and posts articles to newsgroups. |
| ovdb_recover | Attempts to repair a damaged INN database file. |
| ovdb_upgrade | Attempts to upgrade an existing INN database file. |
| prunehistory | Removes specifies from the history file. |
| pullnews | Retrieves news articles from one news server and forwards them to another news server. |
| rnews | Receives news articles from a news server using a UUCP connection. |
| scanlogs | Summarizes information in the INN log files and performs general cleaning and rotation of the log files. |
| sm | Provides a command-line interface to the article storage manager. |

As you can see in Table 20.1, a number of the INN programs are used to help facilitate the news process on the server. The INN package also contains a number of configuration files that define how articles are handled. Table 20.2 lists and describes these files.

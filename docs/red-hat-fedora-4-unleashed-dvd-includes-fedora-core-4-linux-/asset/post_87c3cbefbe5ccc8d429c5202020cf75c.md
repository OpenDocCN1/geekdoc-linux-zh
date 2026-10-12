
- http://www.kingsmountain.com/ldapRoadmap.shtml—A great set of links and resources across the Internet that explain various aspects of LDAP and its parent protocol, X500.
- http://ldap.perl.org/—The home of the Perl library for interacting with LDAP provides comprehensive documentation to get you started.
- http://www.ldapguru.com/—A gigantic portal for LDAP administrators around the world. From forums dedicated to LDAP to jobs specifically for LDAP admins, this site could very well be all you need.

The definitive book on LDAP is *LDAP System Administration* (O'Reilly), ISBN: 1-56592-491-6. It is an absolute must for the bookshelf of any Linux LDAP administrator. For more general reading, try *LDAP Directories Explained* (Addison-Wesley), ISBN: 0-201-78792-X. It has a much stronger focus on Microsoft's Active Directory LDAP implementation, though.

## CHAPTER 28

## News Servers and Mailing Lists

### IN THIS CHAPTER

- Types of News Servers
- The INN Package and Configuration Files
- Installing the INN Package
- Configuring innd
- Reference

There are many advantages to hosting your own local news server. If you have a number of clients on your network who need frequent access to a central site of information or you need to provide employees with a central collaboration site or forum, news servers can provide a simple way of getting information to them in a public and easy-to-use way.

News servers are notoriously difficult to configure and deploy, but follow the information in this chapter and you will be able to avoid many of the problems that are frequently encountered.

### Types of News Servers

The InterNetNews (INN) package is the most popular news server software on Unix servers. The Internet Software Consortium (ISC) currently maintains it, along with the INN website (http://www.isc.org/products/INN/). The Fedora Core Linux distribution includes the INN package as a standard RPM file.

The following sections describe how the INN package works, how to install it, and how to configure it as a local news server. Because some users consider news servers to offer the greatest server-configuration challenges, these sections are quite detailed. The information you learn here will help you avoid some of the common pitfalls while configuring your local news server.

Unless you are an Internet service provider (ISP) or are planning to provide news services to a large group of people, you will likely not be setting up or administering a news server for your own use.

You can use a number of methods to implement a news server on a network, and the way you intend to use the news server determines how you must configure it. The following sections describe three of the most popular types of news servers on local networks: full newsfeed servers, leaf node servers, and local news servers.

### Full Newsfeed Servers

A *full newsfeed news server* receives all the available Usenet newsgroup postings from an upstream news server (a large, commercial server). Because it receives all the newsgroups, it can serve as an upstream news server for other sites and provide newsfeeds to other servers. The other servers themselves might or might not subscribe to all the newsgroups. Besides providing newsfeeds for other sites, the full newsfeed news server can also support newsreader clients that connect to the news server to read and post articles to newsgroups.

Each news server receives newsfeeds and forwards postings to one or more remote news servers. The full newsfeed server must have enough storage capacity to maintain the newsfeeds for all the newsgroups it services. If the remote news servers don’t connect to download their newsfeeds on a daily basis, the newsfeed server must be capable of maintaining all the newsfeeds for the intervening days. This can require a very large amount of data storage capacity beyond the capabilities of systems that are common among home users and many businesses.

### Leaf Node Servers

A *leaf node news server* receives newsfeeds only from upstream news servers: It doesn’t feed other news servers. This is the most common configuration for corporate news servers. Because the leaf node server doesn’t have to feed other news servers, it doesn’t have to retrieve all the newsgroups from its upstream newsfeed. You can pick and choose which newsgroups the news server retrieves from the newsfeed. The main role of the leaf node news server is to provide news services to newsreader clients:

The leaf node does, however, have to maintain a system for users to connect to the news server to read and post messages. This is often done using Unix, Microsoft Windows, or Apple Macintosh workstation software. Each client must connect to the leaf node to download articles from specific newsgroups, and it must upload postings made to the newsgroups. The leaf node must be capable of forwarding new postings to the newsfeed server.

### Local News Servers

An organization that doesn’t want to participate in the worldwide Usenet newsgroups still might want to use Usenet software to create its own news server to handle internal communications within the organization. Usually these communications need to remain private to the organization and don’t need to be sent to all the Usenet newsfeed hosts around the world. This is likely the most common use of a news server you might be asked to configure.

Two methods are used to implement a local news server. An organization might create a standalone news server that doesn't receive any newsfeeds from Usenet servers. The server contains only local newsgroups that are used for internal corporate communications. Alternatively, on a Usenet news server you can create local newsgroups that aren't forwarded through any newsfeeds in the Usenet system. This enables organizations to create their own local newsgroups that their employees can participate in without sharing their information with the rest of the world.

Thus, local newsgroups can be created on news servers that either aren't connected to the Usenet network or that are connected to the Usenet network but do not forward the local groups to their upstream newsfeeds. Any postings to the local newsgroups appear only on the local news server. The Usenet news servers enable clients to post articles to both the local and Usenet newsgroups. However, only the articles posted to Usenet newsgroups are forwarded to the upstream news server. The local articles remain on only the local news server.

### The INN Package and Configuration Files

The INN package (which is formed around the `innd` daemon) contains many executable programs and configuration files that enable the Fedora Core Linux server to work as a network news server. The standard INN RPM package contains all the files necessary for the installation. Table 28.1 describes some of the INN programs included in the distribution, in the order in which you'll find them in the file.

TABLE 28.1 \ \ INN Package Program Files

| Program File | Description |
| --- | --- |
| ctlinnd | Allows the user to manually send control messages to the innd program |
| getlist | Obtains a list of newsgroups from a news server |
| grep history | Queries the history database files for a specific message ID value and returns the record information |
| inncheck | Examines INN configuration files and databases |
| innconval | Prints the values of parameters that are specified in the innd command line |
| innd | Handles all incoming newsfeeds and spawns INN programs as necessary |
| inndstart | Starts the innd daemon from the news user ID |
| innreport | Summarizes INN log files into readable reports |
| innstat | Prints a snapshot of the current status of the INN system |
| innwatch | Monitors the running INN system and, if necessary, throttles the newsfeeds to help reduce the load on the news server |
| mailpost | Manually sends a mail message into a specified newsgroup |
| makedbz | Creates binary indexed database files from the history file |
| makehistory | Creates a text history file of message IDs seen by the news server |
| news.daily | Runs as a cron job to perform daily maintenance on the news server |
| nnrpd | Communicates with newsreaders via the innd daemon |
| nntpgget | Connects to a remote news server and retrieves articles that are specified on the standard input |
| nntpsend | Connects to a remote news server and posts articles to newsgroups |

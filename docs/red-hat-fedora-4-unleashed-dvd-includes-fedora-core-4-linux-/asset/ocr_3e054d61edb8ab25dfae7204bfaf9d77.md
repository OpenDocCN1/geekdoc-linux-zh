You can use a number of methods to implement a news server on a network, and the way you intend to use the news server determines how you must configure it. The following sections describe three of the most popular types of news servers on local networks: full newsfeed servers, leaf node servers, and local news servers.

# Full Newsfeed Servers

A *full newsfeed news server* receives all the available Usenet newsgroup postings from an upstream news server (a large, commercial server). Because it receives all the newsgroups, it can serve as an upstream news server for other sites and provide newsfeeds to other servers. The other servers themselves might or might not subscribe to all the newsgroups. Besides providing newsfeeds for other sites, the full newsfeed news server can also support newsreader clients that connect to the news server to read and post articles to newsgroups.

Each news server receives newsfeeds and forwards postings to one or more remote news servers. The full newsfeed server must have enough storage capacity to maintain the newsfeeds for all the newsgroups it services. If the remote news servers don’t connect to download their newsfeeds on a daily basis, the newsfeed server must be capable of maintaining all the newsfeeds for the intervening days. This can require a very large amount of data storage capacity beyond the capabilities of systems that are common among home users and many businesses.

# Leaf Node Servers

A *leaf node news server* receives newsfeeds only from upstream news servers: It doesn’t feed other news servers. This is the most common configuration for corporate news servers. Because the leaf node server doesn’t have to feed other news servers, it doesn’t have to retrieve all the newsgroups from its upstream newsfeed. You can pick and choose which newsgroups the news server retrieves from the newsfeed. The main role of the leaf node news server is to provide news services to newsreader clients:

The leaf node does, however, have to maintain a system for users to connect to the news server to read and post messages. This is often done using Unix, Microsoft Windows, or Apple Macintosh workstation software. Each client must connect to the leaf node to download articles from specific newsgroups, and it must upload postings made to the newsgroups. The leaf node must be capable of forwarding new postings to the newsfeed server.

# Local News Servers

An organization that doesn’t want to participate in the worldwide Usenet newsgroups still might want to use Usenet software to create its own news server to handle internal communications within the organization. Usually these communications need to remain private to the organization and don’t need to be sent to all the Usenet newsfeed hosts around the world. This is likely the most common use of a news server you might be asked to configure.

## News and Search Servers

News servers provide Internet users with Usenet news services. They have their own TCP/IP protocol, Network News Transfer Protocol (NNTP). On most Linux systems, including Red Hat, the InterNetNews (INN) news server provides news services (www.isc.org). In addition, servers exist that provide better access to Internet resources. The search and indexing server ht://Dig enables document searches of Web and FTP sites (www.htdig.org). With it, you can index documents and carry out complex search requests.

### News Servers: INN

The InterNetNews (INN) news server accesses Usenet newsfeeds, providing news clients on your network with the full range of newsgroups and their articles. Newsgroup articles are transferred using NNTP, and servers that support this protocol are known as NNTP servers. INN was written by Rich Salz and is currently maintained and supported by the Internet Software Consortium (ISC). You can download current versions from its Web site at www.isc.org. INN is also included with most Linux distributions. The documentation directory for INN in /usr/share/doc contains extensive samples. The primary program for INN is the innd daemon.

### INN Configuration Files

Various INN configuration files can be found in /etc/news, including inn.conf, storage.conf, readers.conf, and incoming.conf (see Table 26-1). inn.conf sets options for INN, and the incoming.conf file holds the hosts from which you receive newsfeeds. Place entries for remote hosts in the readers.conf file to allow them access to your news server. Actual newsfeeds are managed in directories in the /var/spool/news directory. Here you will find directories such as article, which holds newsgroup articles; outgoing for articles being posted by your users to newsgroups; and overview, which holds summary information about articles. Correct configuration of INN can be a complex and time-consuming process, so be sure to consult references and online resources, such as the documents. When you change configurations, be sure to restart the INN server. An innd script is in the /etc/rc.d/init.d directory, which has similar arguments to the Web httpd script. You can use start, restart, and stop arguments with the innd script to start, restart, and stop the INN server.

**TABLE 26-1 INN Configuration Files**

| File | Description |
|---|---|
| inn.conf | General INN configuration file. |
| incoming.conf | Specifies hosts from which newsfeeds are received. |
| cycbuff.conf | Configures buffers used in cnfs storage format. |
| storage.conf | Defines storage classes. These consist of a storage method and the newsgroups that use it. Storage methods are the storage formats: tradspool, timehash, timecaf, and cnfs. An additional method, trash, throws out the articles. |
| expire.ctl | Sets the expiration policy for articles on the news server. |
| readers.conf | Designates hosts whose users can access the news server with newsreaders. |
| ovdb.conf | Configures ovdb storage method for overviews. |
| newsfeeds | Defines how your news server feeds articles to other news servers. |
| moderated | Moderated newsgroups. |
| innfeed.conf | Configures newsfeed processes for innfeed. |
| innreport.conf | Configures innreport utility for generating log-based reports. |
| buffindexed.conf | Configures overview buffer for buffindexed method. |

> Tip: There is a man page for each configuration file in INN, providing detailed information on how to configure their features.

#### inn.conf

On many distributions, a basic inn.conf file is already set up for you with default settings. Several of the initial parameters you will have to set yourself, such as domain, which holds the domain name for your server; pathhost, in which you specify the name for your newsreader as you want it to appear in the Path header field for news articles you post; and server, in which you specify your newsreader's IP or fully qualified domain name address, as in mynews.mytrek.com. Different Path options have already been set up for you defining the location of different INN directories, such as patharticles set to /var/spool/news/articles that holds your newsgroup articles, and pathetc set to /etc/news for your configuration files.

#### Storage Formats

Storage formats for the vast number of news articles that are often downloaded and accessed are a central concern for a full-scale news server like INN. INN lets you choose among four possible storage formats: tradspool, timehash, timecaf, and cnfs. tradspool is the traditional method whereby articles are arranged in a simple directory structure according to their newsgroups. This is known to be very time-consuming to access and store. timehash stores

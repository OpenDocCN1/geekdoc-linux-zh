# # Chapter 22

# ## Setting Up a News Server

# **In This Chapter**

+   - Understanding news transports
+   - Planning your news server
+   - Configuring an INN news server
+   - Setting up news feeds
+   - Choosing how articles are stored
+   - Setting up expiration times
+   - Allowing access to your server

Newsgroups, the first popular offshoots of the early success of Internet e-mail, were started by people with common interests collectively maintaining e-mail lists to exchange messages on their subjects. As the lists became larger and harder to maintain, a new solution was needed. The result was Usenet newsgroups.

Today, with literally thousands of newsgroups available (more than 41,800 newsgroups are listed officially with the Internet Software Consortium: www.isc.org), managing the servers that gather newsgroups and offering the newsgroups to people in an organization can be a daunting task. The difficulty of the task relates more to making decisions about which newsgroups to offer and how you want to manage news feeds with other servers than it does to implementing those decisions (although that is tricky, too).

This chapter describes how to set up a news server on your Red Hat Linux system. It focuses on the most popular news server software — InterNetworKNews (or INN configuration files). INN is free and comes with Red Hat Linux.

Many other configuration files and methods of setting up a news server exist than those that are contained in this chapter. Use this chapter as a jumping-off point for configuring your news server. Then, refer to documents and sample files in /usr/share/doc/inn* and the configuration files themselves for more information on setting up your news server.

# ### Understanding News Transports

In Red Hat Linux, the innd and the nnrpd daemons handle news transports. The innd daemon handles the incoming news feeds. When users request newsgroup articles, the innd daemon starts a nnrpd process to handle the request.
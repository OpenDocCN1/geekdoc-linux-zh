Depending on the newsgroups you want to receive and the number of days you want to retain articles, you have to set aside appropriate disk space to hold the articles. The newsgroups are stored in a directory hierarchy (based on the newsgroup names) in the /var/spool/news directory of your system. If you’re setting up a news server, you may want to devote a large disk partition to the /var/spool/news directory.

In your news server’s configuration files, enter the name of the server providing the news feed. At the same time, add to the configuration files the names of any downstream news servers (if any) that receive news feeds from your server. Then you can start the news server and wait for news to arrive. Monitor the log files to ensure that the news articles sort and store properly in the /var/spool/news directory on your system.

When you have news up and running, you must run news maintenance and cleanup scripts by running the *cron* jobs. On Fedora Core, a *cron* job is already set up to run the /usr/bin/news.daily script to perform the news maintenance tasks.

In the following sections, I introduce you to INN setup, but you can find out more about INN from the Internet Software Consortium (ISC), a nonprofit corporation dedicated to developing and maintaining open source Internet software, such as BIND (an implementation of Domain Name System), DHCP (Dynamic Host Configuration Protocol), and INN. Rich Salz originally wrote INN; ISC took over the development of INN in 1996. You can find out more about INN and can access other resources at ISC’s INN Web page at *www.isc.org/products/INN*.

# InterNetNews components

INN includes several programs that deliver and manage newsgroups. It also includes a number of files that control how the INN programs work. The most important INN programs are the following:

+   *   *innd*: The news server. It runs as a *daemon*—a background process that keeps itself running to provide a specific service—and listens on the NNTP port (TCP port 119). The *innd* server accepts connections from other feed sites, as well as from local newsreader clients, but it hands off local connections to the *nrrpd*.
+       *   *nrrpd*: A special server invoked by *innd* to handle requests from local newsreader clients.
+       *   *expire*: Removes old articles based on the specifications in the text file /etc/news/expire.ctl.
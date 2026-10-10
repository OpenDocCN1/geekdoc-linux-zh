typically take such steps as prohibiting most of the `alt.binaries` groups and setting the article expiration times to a rather short value in the `/etc/news/expire.cn` file. The sooner you can get them off your server, the sooner replacements can be brought in.

An emergency feature included in `/usr/sbin/ctlinnnd` is *throttling*, which can either reduce the transfer capabilities between newsfeed servers during floods or batches or sever all connections! Only with careful monitoring will you know whether throttling your INN server is needed to prevent a possible disk overload or system saturation.

Finally, if for any reason your `/etc/services` file is compromised, your Linux kernel may not understand the mapping of TCP/IP port 119 to NNTP, so it is suggested that you keep that file backed up along with your INN files.

After installing and configuring INN and notifying your ISP that you want to access their NNTP service, you should be able to use INN to download news and access it with a newsreader (assuming that you've granted yourself permission in the `nrcp.access` file). A lot of complexity can be introduced into INN's configuration file, but keeping it simple tends to be the best method. As your experience grows, you can modify the behavior of the newsfeeds.

# The tin Newsreader

Many newsreaders are available for Linux systems. Your OpenLinux distribution includes `tin`—a simple yet fast and efficient newsreader for Linux. You might not need a newsreader at all if you have Web services on your system. Many Web browsers allow access to newsgroups either in your own news directory or through a connection to an ISP's newsfeed.

The primary advantage of `tin` over earlier newsreaders like the `rn` (read news) package is that `tin` lets you follow threads. A *thread* in a newsgroup is a continuing discussion on one primary subject. Before threaded newsreaders became available, you had to read news in consecutive order from first to last, trying to assemble several different conversations into logical groups as you went. With `tin`, you can start with one thread or subject and read all the postings about that subject and then move on to another subject, regardless of the chronological order in which the postings were made.

Threads are usually handled automatically so that they require no special user interaction, although there is some work performed behind the scenes on your newsfeed. Some newsgroups do not support threading, but most do. If threads are available, you can follow the thread from start to finish, or jump out and change threads at any time.

![](bbox=[0.88, 0.825, 0.93, 0.86])

![](bbox=[0.94, 0.85, 0.99, 0.98])
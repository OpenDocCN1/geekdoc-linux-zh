# Configuring and Starting the INN Server 667

+   - nntpsend: Invokes the innxmit program to send news articles to a remote site using NNTP. The configuration file /etc/news/nntpsend.ctl controls the nntpsend program.

+   - cllind: Enables to control the innd server interactively. The cltinnd program can send messages to the control channel of the innd server.

The other vital components of INN are the control files. Most of these files are in the /etc/news directory of Fedora Core system, although a few are in the /var/lib/news/ directory. Between those two directories, you have more than 30 INN control files. Some important files include the following:

+   - /etc/news/inn.conf: Specifies configuration data for the innd server. (To view online help for this file, type man inn.conf.)

+   - /etc/news/newsfeeds: Specifies what articles to feed downstream to other news servers. (The file is complicated, but you can get by help by typing man newsfeeds.)

+   - /etc/news/incoming.conf: Lists the names and addresses of hosts that provide news feeds to this server. (To view online help for this file, type man incoming.conf.)

+   - /etc/news/storage.conf: Specifies the storage methods to be used when storing news articles. (To view online help for this file, type man storage.conf.)

+   - /etc/news/expire.ctl: Controls expiration of articles, on a newsgroup level, if desired. (To view online help for this file, type man expire.ctl.)

+   - /var/lib/news/active: Lists all active newsgroups, showing the oldest and newest article for each, and each newsgroup's posting status. (To view online help for this file, type man active.)

+   - /var/lib/news/newsgroups: Lists newsgroups, with a brief description of each.

+   - /etc/news/readers.conf: Specifies hosts and users that are permitted to read news from this server and post news to newsgroups. The default file allows only the localhost to read news; you have to edit it if you want to allow other hosts in your local area to read news. (To view online help for this file, type man readers.conf.)

In the next few sections, I describe how to set up some of the important control files.

| Book VIII |
| Chapter 4 |
| Mail and News |
| Serving Up |
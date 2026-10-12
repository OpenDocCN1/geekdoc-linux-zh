
In the following sections, I introduce you to INN setup, but you can learn more about INN from the Internet Software Consortium (ISC), a nonprofit corporation dedicated to developing and maintaining open source Internet software, such as BIND (an implementation of Domain Name System), DHCP (Dynamic Host Configuration Protocol), and INN. Rich Salz originally wrote INN; ISC took over the development of INN in 1996. You can learn more about INN and can access other resources at ISC's INN Web page at www.isc.org/products/INN.

## InterNetNews components

INN includes several programs that deliver and manage newsgroups. It also includes a number of files that control how the INN programs work. The most important INN programs are the following:

- `innd` — The news server. It runs as a `daemon` — a background process that keeps itself running to provide a specific service — and listens on the NNTP port (TCP port 119). The `innd` server accepts connections from other feed sites, as well as from local newsreader clients, but it hands off local connections to the `nnrpd`.
- `nnrpd` — A special server invoked by `innd` to handle requests from local newsreader clients.
- `expire` — Removes old articles based on the specifications in the text file `/etc/news/expire.ctl`.
- `nntpsend` — Invokes the `innxmit` program to send news articles to a remote site by using NNTP. The configuration file `/etc/news/nntpsend.ctl` controls the `nntpsend` program.
- `ctl innd` — Enables you to control the `innd` server interactively. The `ctl innd` program can send messages to the control channel of the `innd` server.

The other vital components of INN are the control files. Most of these files are in the `/etc/news` directory of your Red Hat Linux system, though a few are in the `/var/lib/news` directory. Between those two directories, you have over 30 INN control files. Some important files include the following:

- `/etc/news/inn.conf` — Specifies configuration data for the `innd` server. (To view online help for this file, type `man inn.conf`.)
- `/etc/news/newsfeeds` — Specifies what articles to feed downstream to other news servers. (The file is complicated, but you can get help by typing `man newsfeeds`.)
- `/etc/news/incoming.conf` — Lists the names and addresses of hosts that provide news feeds to this server. (To view online help for this file, type `man incoming.conf`.)
- `/etc/news/storage.conf` — Specifies the storage methods to be used when storing news articles. (To view online help for this file, type `man storage.conf`.)
- `/etc/news/expire.ctl` — Controls expiration of articles, on a per-newsgroup level, if desired. (To view online help for this file, type `man expire.ctl`.)
- `/var/lib/news/active` — Lists all active newsgroups, showing the oldest and newest article number for each, and each newsgroup's posting status. (To view online help for this file, type `man active`.)
- `/var/lib/news/newsgroups` — Lists newsgroups, with a brief description of each.
- `/etc/news/readers.conf` — Specifies hosts and users that are permitted to read news from this news server and post news to newsgroups. The default file allows only the `localhost` to read news; you have to edit it if you want to allow other hosts in your local area network to read news. (To view online help for this file, type `man readers.conf`.)

In the next few sections, I describe how to set up some of the important control files.

## The inn.conf file

This file holds configuration data for all INN programs — which makes it the most important file. Each line of the file has the value of a parameter in the following format:

```
parameter:    value
```

Depending on the parameter, the value is a string, a number, or true or false. As in many other configuration files, comment lines begin with a hash sign (#).

Most of the parameters in the default inn.conf file in the /etc/news directory should not require changes. You may want to edit one or more of the parameters shown in Table 4-2.

**Table 4-2 Configuration Parameters in /etc/news/inn.conf**

| Parameter Name | Description |
|---|---|
| mta | Set this to the mail transfer agent that will be used by innd to transfer messages. The default is to use sendmail. |
| organization | Set this to the name of your organization in the way you want it to appear in the Organization: header of all news articles posted from your system. Users may override this by defining the ORGANIZATION environment variable. |
| ovmethod | Sets the type of overview storage method (the overview is an index of news articles in the newsgroup). The default method is tradindexed, which is fast for reading news, but slow for storing news items. |
| pathhost | Set this to the name of your news server as you want it to appear in the Path header of all postings that go through your server. If pathhost isn't defined, the fully qualified domain name of your system is used. |
| pathnews | Set this to the full pathname of the directory that contains INN binaries and libraries. In Red Hat Linux, pathnews is set to /usr/lib/news. |
| domain | Set this to the domain name for your server. |
| allownewnews | Set this to true if you want INN to support the NEWNEWS command from newsreaders. Because this command can drastically reduce your server's performance, INN documentation recommends that you set this to false. |
| storageapi | Set this to true if you want articles to be stored using the Storage Manager API (application programming interface). The default setting of false causes INN to use the traditional article-storage method of storing one article per file. If you set this to true, you have to choose between the storage methods timehash and cnfs, and you have to create new spool and database files (type man storage.conf to read more about cnfs and timehash storage methods). For a small number of newsgroups, you can leave this option at its default value of false. |
| hiscachesize | Set this to the size in kilobytes that you want INN to use for caching recently used history file entries. The default setting of 0 disables history caching. Because history caching can greatly increase the number of articles your server can process per second, you may want to set a value of 16384 (for 16MB). |
| innflags | Set this to any flags you want to pass to the INN server process when it starts up. |

## The newsfeeds file

The newsfeeds file specifies how incoming news articles are redistributed to other servers and to INN processes. If you provide news feeds to other servers, you have to list these news feeds in this file. (You also must have an entry labeled ME, which serves a special purpose that I explain later in this section.)

The newsfeeds file contains a series of entries, one for each feed. Each feed entry has the following format:

```
site[/exclude,exclude...]
:pattern.pattern...[/distrib,distrib...]\
:flag,flag...\
:param
```

Each entry has four fields separated by colons (:). Usually, the entries span multiple lines, and a backslash (\ ) at the end of the line is used to continue a line to the next. Here's what the four fields mean:

- The first field, site, is the name of the feed. Each name must be unique, and for feeds to other news servers, the name is set to the host name of the remote server. Following the name is an optional slash and an exclude list (/exclude,exclude...) consisting of a list of names. If any of the names in this list appear in the Path line of an article, that article won't be forwarded to the feed. You can use an exclude list if you don't want to receive articles from a specific source.
- The second field consists of a comma-separated list of newsgroup patterns, such as *@alt.binaries.warez.*,!control*,!local*, followed by an optional distribution list. The distribution list is a list of comma-separated keywords, with each keyword specifying a specific set of sites to which the articles are distributed. The newsgroup patterns essentially define a subscription list of sites that receive this news feed. An asterisk matches all newsgroups. A pattern beginning with an @ causes newsgroups matching that pattern to be dropped. A pattern that begins with an exclamation mark (!) means the matching newsgroups are not sent. By the way, the simple pattern-matching syntax used in INN configuration files is referred to as a wildmat pattern.
- The third field is a comma-separated list of flags — fields that determine the feed-entry type and set certain parameters for the entry. There are numerous flags; type man newsfeeds and read the man page for more information about the flags.
- The fourth field is for parameters whose values depend on the settings in the third field. Typically, this field contains names of files or external programs that the INN server uses. You can learn more about this field from the newsfeeds man page.

Now that you know the layout of the /etc/news/newsfeeds file, you can study that file as an example. The default file contains many sample feed entries, but only two are commented out:

- ME is a special feed entry that's always required. It serves two purposes. First, the newsgroup patterns listed in this entry are prepended to all


newsgroup articles to forward to each news server (based primarily on what they will accept). You can also set up definitions that apply to groups of servers.

> **NOTE:** Despite its name, a news feed doesn't actually feed news articles to another site. It simply reports that an article is available to be transferred to the other news server.

Within the entries in the newsfeeds file, certain wildcard characters can be used to match or exclude whole sets of newsgroups. You can probably figure out how they work in the context of the examples. If not, however, you can refer to the “Understanding Wildmat Characters” sidebar for information on using the wildcard characters.

### Understanding Wildmat Characters

When you need to identify newsgroups in your newsfeeds configuration file, you can use several different wildcard characters to simplify the process. These characters are defined on the wildmat man page (type `man wildmat`). Here is what they do:

- `!`: The exclamation point is used to indicate that the newsgroup name that follows should not be matched.
- `*`: An asterisk at the end of a newsgroup name indicates that all newsgroups following the one shown (those lower in the hierarchy) should be matched.
- `[abc]`: Any single character surrounded by the brackets is matched. For example, `[abc]*` matches any group name that begins with a, b, or c. You can also specify number or letter ranges, such as 3–9 or a–r, with the braces to include all those numbers or letters.
- `?`: A question mark matches any single character. So, `c?mp` matches comp, camp, and a lot of stuff that makes no sense at all.
- `[^abc]`: When a `^` is placed at the beginning of a set of brackets, the letters in the pattern match any character that is not in the brackets. For example, `[^abc]*` matches any group that does not begin with a, b, or c.

The default /etc/news/newsfeeds file has only an ME parameter entry in it and a controlchan entry (and a lot of comments). The ME entry is required; you can have only one of them in your newsfeeds file, and it must appear before any other news feed lines. This entry contains a subscription list that is automatically added first to the subscription list of every other entry. Here is the default ME line:

```
ME:!*/!local,!collabra-internal::
```

This default ME line specifically indicates some articles that are not forwarded. This line causes all incoming articles with local or collabra-internal in the Path header to be rejected. Articles that come in with either of those headers indicate that they are coming from a misconfigured server.

> **NOTE:** The ME subscription entry defines only the subscription lists that you feed. It has nothing to do with the newsgroups that you receive. Newsgroups that you receive are defined in the active list. See the active(5) man page.

The following is an example of an ME entry that includes additional restrictions:

```
ME\
:*,@alt.binaries.warez.*,!junk,!control*,!local*,!foo.*\
/world,usa,na,gnu,bionet,pubnet,u3b,enet,vmsnet,inet,ddn,k12\
::
```

With this entry, all newsgroups are propagated to every server, with the exception of junk, control, local, and foo groups. The exclamation mark indicates that the name that follows is to be excluded.

With the ME line set, you can go about defining how your specific news feeds are done. Here is an example of an innfeed! line you can add to your newsfeeds file. This example funnels all news feeds to the startinnfeed command.

```
innfeed!:\
! * \
:Tc,Wnn*, $16384:/usr/bin/startinnfeed -y
```

This line runs the startinnfeed command to start the innfeed program. The innfeed program, in turn, carries out the actual transfer of news articles between the news servers.

> **NOTE:** If you have used an earlier version of INN, you should note that the overchan and crosspost programs are no longer used. The functions they used to perform are now incorporated into the INN server. With useoverchan set in the inn.conf, you can still use overchan. However, crosspost is no longer supported.

After the ME and innfeed! entries, you need to add entries that define the actual news servers to which you will feed articles. You should have one entry for each news server that you feed. The general format of those entries is as follows:

```
remote-peer.domain.com/name-in-header.domain.com\
:newsgroup-list\
:Tm;innfeed!
```

You need to replace remote-peer.domain.com with the FQDN of the server that you are feeding the news to. Next, replace the name-in-header with any alias names that the remote news server uses. The aliases are names that the remote news server puts in the Path header of the articles it forwards. (If no aliases exist, leave off the entire /name-in-header part.) You need to enter a newsgroup-list only if you want to feed newsgroups that are different from the newsgroups that are set by default (in your ME entry). The last part of the entry (:Tm;innfeed!) should be left as it is.

If your server has the controlchan feature turned on (usecontrolchan: true in the inn.conf file), you can use the entry for the controlchan program in the newsfeeds file or create your own entry. The default entry is meant to reduce the load if, in a short period of time, many control messages arrive at your news server. This entry runs the /usr/bin/controlchan command.

```
controlchan!
    :!*,control,control.*,!control.cancel\
        :Tc,Wnsm:/usr/bin/controlchan
```

You can use a mind-numbing number of options within the newsfeeds file. If you are interested in delving deeper, read the comments in the newsfeeds file and refer to the newsfeeds manual page (type `man newsfeeds`). That manual page will also point you to related man pages.

## Getting a List of Active Newsgroups

The Internet Software Consortium (www.isc.org) maintains a listing of all officially active newsgroups. ISC stores these newsgroups in two different files: newsgroups and active. The newsgroups file contains each newsgroup name and a short description of the newsgroup. The active file stores the newsgroups to indicate which newsgroups your computer will offer.

There are two ways you can go about creating your newsgroups and active files. For a minimal news server, you can use the default newsgroups and active files in /var/lib/news and add the information you want. Then you can add newsgroups later using the ctlnnnd newsgroup command. Alternatively, you can get complete active and newsgroups files from ISC and edit those down.

You can download the latest copies of the active and newsgroups files from the ISC FTP server: ftp://ftp.isc.org/pub/usenet/CONFIG/. From that directory, you can download either uncompressed versions of those files (each is more than 1MB in size) or compressed versions. Choose the active.gz and newsgroups.gz files, which you can uncompress in Red Hat Linux by using the gunzip command (`gunzip active.gz newsgroups.gz`).

Place both the active and newsgroups files in your /var/lib/news directory (or whatever directory you changed your pathdb parameter to in the inn.conf file). The newsgroups file provides the names and descriptions of the newsgroups offered to the users of your news server. The active file is the official list of newsgroups that is read by the innnd daemon so that it knows what newsgroups it should accept articles for. You can edit the active file manually.

The active and newsgroups files need to be owned by the news user. So you should either copy those files to your /var/lib/news directory while you are logged in as the news user or change their ownership by typing the following with the files in the current directory:

```
# chown news.news active newsgroups
```

## Creating the History Database

Before you can start your INN server, you need to create the history database. You can do this from the /var/lib/news directory by typing the following (while logged in as the news user):

```
$ touch history
$ makedb -i
$ mv history.n.dir history.dir
$ mv history.n.hash history.hash
$ mv history.n.index history.index
$ chmod 644 history*
```

## Choosing How Articles Are Stored

Traditionally, news servers have stored newsgroup articles in a very simple format. In the news spool directory (such as /var/spool/news), each article was stored under a subdirectory named after the newsgroup. For example, articles for the comp.os.linux.x newsgroup would be stored in the directory comp/os/linux/x in the news spool directory. Each article would be named by its unique message number and placed in that directory.

Unfortunately, the traditional way of storing news articles has become quite inefficient, given the huge volume of newsgroup articles these days. In addition to the traditional method, the INN news server offers the following other methods for storing newsgroup articles:

- **timehash:** Articles are stored in directories based on when they arrive. This method makes it easier to control how long articles are kept and prevents any directory from containing too many files.
  - In the default news directory (/var/spool/news), the timehash method of storage creates directories based on the time articles are received. A timehash directory is in the form time-xx/bb/cc/yyy-aadd. Here, xx is a hexadecimal value of the storage class, and yyyy is a hexadecimal value of a sequence number. The other values represent the arrival time.
- **cnfs:** Articles are stored in buffer files that are configured before articles arrive. In this arrangement, when a new article arrives and the buffer is full, the new article replaces the oldest article. This is referred to as cyclical storage.
  - When buffers are used instead of the file system, articles can be stored and served much faster. The downside to this method is that, because articles are overwritten automatically after the buffer limit is reached, it is harder to enforce a policy that retains articles for a set period of time. This method also requires more upfront configuration.
- **timecaf:** Lots of articles are stored in a single file with this storage method. This method can be about four times faster than the timehash method, though it gives you less

| Flag | Description |
|---|---|
| *W<items>* | A list of one or more items to write: b (article size in bytes), f (the full path of an article), g (the first newsgroup of an article posting), h (the message ID hash of an article), m (the message ID), n (the relative path of an article), p (the posted time of an article), s (the site that fed the article), t (the time an article was received), * (the names of funnel feed-in's or all sites that receive the article), N (the newsgroups header of an article), d (the distribution header of an article), H (all headers of an article), o (the overview data of an article), P (the path header of an article), R (an article’s replication information). |

The fourth field is a multi-purpose parameter. Its usage depends on the type of flags used in the third field.

# SAMPLE newsfeeds ENTRIES

The newsfeeds file controls how articles posted on the local site are fed out to other NNTP servers. Because of the inherent complexity of entries in the newsfeeds file, the easiest way to grasp how to use entries is to analyze some sample entries.

First, consider the following entry:

```
ME:*:!junk,!control*,!local*\
/world,usa,na,gnu,bionet,pubnet,u3b, eunet,vmsnet,inet,ddn,k12::
```

Every newsfeeds file requires a single ME site entry. This entry lists a set of defaults that affect all other entries in the newsfeeds file. The subscription list from the ME entry is automatically added to the start of the subscription list for all other entries. In this example, the subscription list is *;!junk,!control,!local*/world,usa,na,gnu,bionet,pubnet,u3b, eunet,vmsnet,inet,ddn,k12. This subscription list has two parts: the part before the forward slash and the exceptions list after the forward slash.

The part before the forward slash is *;!junk,!control,!local*. This indicates that local postings, control postings, and junk postings are not propagated unless a group is explicitly indicated in an entry’s subscription list.

If a distribution field appears in a ME entry, only articles which match the distribution list are accepted and all other articles are rejected.

In addition to the required ME entry, several special entries provide the program feeds for the overchan, innfeed, controlchan, and crosspost utilities. These entries are provided with the default newsfeeds file and can simply be uncommented if you need to use them.

For the traditional storage method, uncomment the following entries:

```
overview!*:Tc,WO:/usr/local/news/bin/overchan
crosspost!*:Tc,Ap,WR:/usr/local/news/bin/crosspost
innfeed!*:Tc,Wnm,S16384:/usr/local/news/bin/startinnfeed -y
```
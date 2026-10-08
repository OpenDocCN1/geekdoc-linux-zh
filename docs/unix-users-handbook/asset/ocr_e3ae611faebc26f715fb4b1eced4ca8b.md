# grep

![](bbox=[0.04, 0.19, 0.12, 0.31])

Here in the information age, we have too much information. We are constantly trying to extract the information we are after from stacks of information. The **grep** command is used to search for text and display it. **grep** stands for General Regular Expression Parser. Let's first look at a few simple searches and display the output with **grep**. Figure 10-8 shows creating a long listing for /home/denise, and using **grep**, we search for patterns.

```
```
$ ls -a /home/denise | grep netscape
.netscape-bookmarks.html
.netscape-cache
.netscape-history
.netscape-newsgroups-news.sprry.com
.netscape-newsgroups-newsserv.hp.com
.netscape-preferences
$ ls -a /home/denise | grep -c netscape
6
$ ls -a /home/denise | grep NETSCAPE
$ ls -a /home/denise | grep -i NETSCAPE
.netscape-bookmarks.html
.netscape-cache
.netscape-history
.netscape-newsgroups-news.sprry.com
.netscape-newsgroups-newsserv.hp.com
.netscape-preferences
$ ls -a /home/denise | grep -F "netscape
> ,c"
.cshrc
.cshrc.orig
.netscape-bookmarks.html
.netscape-cache
.netscape-history
.netscape-newsgroups-news.sprry.com
.netscape-newsgroups-newsserv.hp.com
.netscape-preferences
.newsrc-news.sprry.com
.newsrc-newsserv.hp.com
$ 
```
```

Figure 10-8 grep Command
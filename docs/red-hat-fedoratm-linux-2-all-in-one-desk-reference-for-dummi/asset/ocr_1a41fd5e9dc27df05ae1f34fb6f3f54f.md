to create an initial history database, associated indexes, and set the ownership and permissions of some files:

```
/usr/lib/news/bin/makehistory -b -f history -0 130000 -Icd /var/lib/news /usr/lib/news/bin/makedbz -s 'wc -l < history' -f history chown news.news *
chown news.news /var/spool/news/overview/group.index
chmod 664 /var/spool/news/overview/group.index
```

As with any other servers in Fedora Core, to start innd, log in as root and type the following command:

```
service innd start
```

To ensure that innd starts at boot time, type the following command:

```
chkconfig --level 35 innd on
```

![](bbox=[0.14, 0.44, 0.22, 0.49])

If you change any configuration file (such as innd.conf or newsfeeds), restart the innd server with the following command:

```
service innd restart
```

Type ps ax to see if the innd process is up and running. If all goes well, you see two processes, such as the following, listed in the output of the ps ax command:

```
23789 ? S 0:00 /usr/lib/news/bin/innd -p4
23794 ? S 0:00 /usr/bin/perl /usr/lib/news/bin/controlchan
```

![](bbox=[0.14, 0.66, 0.22, 0.71])

The /var/log/spooler file contains all status and error messages from innd. Type the following command to see the last few messages in that file:

```
tail /var/log/spooler
```

# Setting Up Local Newsgroups

If you want to use newsgroups as a way to share information within your company, you can set up a hierarchy of local newsgroups. Then you can use these newsgroups to create virtual communities within your company, where people with shared interests can informally discuss issues and exchange knowledge.
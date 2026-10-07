When NNTP receives an article from a remote machine, it passes it on to one of the news subsystems that must be in place. Usually, this is news or inews. (You can also use NNTP for batching of articles, explained earlier in this chapter, in which case the relaynews program handles the batch of articles.) NNTP uses the /usr/lib/news/history file to properly perform some protocol transfers, so this file must be configured correctly.

# # Installing the NNTP Server Program

The NNTP server, nntpd, is usually supplied as source code only, as mentioned earlier. Typically, it must be compiled on your machine to include machine-specific information. The configuration of nntpd is performed through a utility program usually stored as /usr/lib/news/common/conf.h. You can search for the program with the command:

```
find / -name conf.h -print
```

Run this program (which is a number of macros) and answer all the questions about your system.

Begin the NNTP installation process by creating a directory in which nntpd can store incoming articles. You should create this directory as /usr/spool/news/.tmp (or /var/spool/news/.tmp). The ownership of the directory must be set to news. The two commands to perform these steps are:

```
mkdir /usr/spool/news/.tmp
chown news.news /usr/spool/news/.tmp
```

The NNTP server can be configured in one of two different modes. The first is as a standalone server, which starts itself from the rc startup files (usually rc.inet2) when the Linux system is booted. Alternatively, nntpd can be configured to be managed through inetd, instead of running all the time.

If you are configuring nntpd to run as a standalone daemon, make sure there is no line in the /etc/inetd.conf file that calls the daemon (this is discussed in a moment). Check the /etc/inetd.conf file for potential conflicts with the nntpd daemon started in the rc files.

If you want to configure nntpd to run through inetd, which can reduce the overall load on your system except when news must be processed, you need to add an entry to the inetd configuration file, usually stored as /etc/inetd.conf. The following line should be added to this file with an ASCII editor:

```
nntp     stream     tcp     nowait     news     /usr/etc/in.nntpd     nntpd
```

There may be a line like this already in the inetd.conf file, commented out. In this case, verify that the line reads the same as the one above and remove the comment symbol.

# 41
CONFIGURING LINUX FOR NEWS
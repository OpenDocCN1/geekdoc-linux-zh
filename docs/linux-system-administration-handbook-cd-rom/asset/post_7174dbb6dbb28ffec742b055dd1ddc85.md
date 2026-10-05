
• Perl Configuration: Defines if perl support is included or not where the perl header and libraries reside.

Once the config.data file is verified to be correct for the current system, compile the news software as an unprivileged user by doing the following:

```
>cd INNSRC
>make world > make.log
```

Assuming all goes well, verify that things will be installed in the correct place by doing

```
>make -n install
```

Then, when confident that all is correct, become root and install the package by doing

```
su - root
#mkdir -p <news spool directory>
#chown news.news <news spool directory>
#chmod 775 <news spool directory>
#cd INNSRC
#sh /makersdir.sh
#.BUILD
```

The makersdir.sh script will create the higher-level directories and give them the correct permissions, and the BUILD script will install all of the files as well as provide a small active file and build a corresponding history file. This initial installation must be done as root to ensure that all of the SUID scripts and wrappers have the correct ownership and permissions. The only files that should be changed at this point are the ones in the INSRC/site directory. From now on, unless the SUID file source is modified, you should be able to do all makes as the news user. In the future, before making any changes, it is wise to preserve the original source files by doing a make backup first. Also make sure to add cron jobs for nntpsend and news.daily when feeds are finally set up.

## 10.4 INN Internals

Before trying to start INN and obtain newsfeeds, you should have a fairly decent understanding of how the news system works. There are many different segments of the IN software that control different aspects of how news is handled. Some of these programs run all the time and some only start when needed or if run by hand. To get an overall picture, we'll start by describing how INN operates under various conditions.

### rc.news

After installing INN, create a script that checks the consistency of the last INN shutdown and then starts the news server back up and performs any other needed cleanup. This is usually own by calling the script provided in $INNSRC/samples/rc.news from an /etc/rc2.d/ file or by running it from /etc/rc2 directly. The rc.news script will read all of the variables from the INN configuration, set the flags that it will pass to instart, and check to see if the server was not shut down cleanly.

It will also ensure that if an expire was being run, the newsmaster will be notified or carries on with the old article removal, as well as verifying the existence of the active and history files. After it ensures that everything is in a stable state, it starts the server and a process called “innwatch” to monitor the machine.

### innwatch

The innwatch program monitors the load average, disk space usage, and number of used modes on the partitions for news use. The innwatch program can be customized for site-specific parameters by modifying the “innwatch.ctl” file located in $INNSRC/site/.

### innd

As described above, rc.news starts the main process, innd, which is the actual daemon that listens for and handles all incoming connections on port 119.

When started, the innd reads the active, newsfeeds, and hosts.nnpt files into memory and then opens a socket on port 119 and starts logging article to the history file and connections to the set of files specified in the /etc/syslog.conf file.

### Logging

Where INN logs is controlled by several files, “/etc/syslog.conf,” the settings in “config.data” before compilation, and in the “control.ctl” file.

The config.data file generally tells INN what the default log directory is and at what level to log various types of messages. The config.data file also defines where the errors and general messages (like all incoming news) should be logged. The control.ctl file tells INN where to log things like newgroup and removegroup as well as other cancel message types. See the section on control messages for more details. The syslog.conf entries tell INN where to log messages of varying severity. Common entries to the syslog.conf would look like the following tab-separated entries:

```
news.crit    /var/log/news/news.crit
news.err      /var/log/news/news.err
news.notice  /var/log/news/news.notice
```

This tells innd it should send messages of the correct severity to the corresponding log file in /var/log/news.

### The Active and History Files

The active and history files are the main INN databases that keep track of what articles are stored or were previously stored on the machine. The “active file” has one line for each newsgroup which contains the newsgroup name, the high and low watermarks for the articles currently stored on the server, and the status of the newsgroups. The newsgroup status is determined at the time of creation and can be one of the following:

- Local postings are allowed.
- Only remote postings are allowed.
- This is a moderated group and all postings must be approved.
- Articles are passed on and filed to the junk newsgroup only if received.
- Articles cannot be posted to this group.
- group.name—Articles are locally filed in the “group.name” group, some-what like a symbolic link for a newsgroup.

Coupled with the active file is the active.times file which provides a chronological log of when newsgroups were created. Each line contains the name of the newsgroup, the time of creation, and, optionally, the E-mail address of the person who created the group.

Equ important is the file that holds the record of all articles currently on the server and those that were on the server but are now expired. The “history file” contains one line for each article with the tab-separated fields being a uniquely identifying Message-ID, date the article was received, and a set of space-separated entries identifying newsgroups the article was posted to. The third field is empty if the article has expired.

Both the history and active files are always opened by the innd process and are updated any time the news server receives a new article or when articles are expired. If one of these files is lost or corrupted, they must be rebuilt from the existing data on the disk. This can be a long and arduous process.

## 10.5 NNRP

The innd receives two kinds of connections on port 119: NNTP (Net News Protocol) and NNRP. NNRP is the protocol used by other news servers to transfer articles in batch. When such a connection is received, innd checks the hosts.mntp and hosts.nttp.nolimit files for the name of the connecting machine.

To allow the feeding machine access to the news server, edit the $INSRC/site/hosts.nttp or $INSRC/site/hosts.nttp.nolimit file and add the feeding machine's name on a line by itself. Comments begin with a pound sign (#), and blank lines are ignored when the file is parsed. The first field of the colon-separated newsfeeds entry is the hostname or IP address of the machine to be fed. The second field is a password that the client machine must provide when first connecting; this field may be left blank and usually. The optional third field is a wildcard-matched listing of newsgroups that will be accepted from the client site. Generally this file is set up with entries that have the client hostname and a colon (news.uu.net).

### rnews

The inews program reads news articles stored in a local queue, typically. A UUCP batch file starts with a pound bang (#!) to indicate that multiple articles are stored in one file. If the pound bang is not present at the beginning of the file, then inews interprets the entire file to be only one article.

### nnrp.access

The nnrp.access file contains entries of colon-separated fields with the pound sign (#) as a comment. The first field of the entry is the hostname or address. The second field is the privileges granted to the client. The third field is a username that must be used. The fourth field, which can also be left blank, is a password that the client must issue.

### inews

If your peer news server is authenticated, the news server will accept all the articles being sent. The innd takes each article separately, logging each to the

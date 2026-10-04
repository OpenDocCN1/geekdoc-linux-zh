
## Installing the News Server

If you install the news server during Fedora Core installation, you don't have to do much more to begin using the news services. Otherwise, you can use the Red Hat Package Manager (RPM) to install the InterNews (INN) — a TCP/IP-based news server.

To check whether INN is already installed, type the following command:

```
rpm -q inn
```

If INN is installed, you see a line similar to this:

```
inn-2.3.5-8
```

If you get a message saying the package isn't installed, you can install it manually from the companion DVD-ROM. Log in as root and insert the DVD-ROM into the DVD-ROM drive. If you're using GNOME or KDE desktop, the DVD-ROM mounts automatically. Otherwise, type the following command to mount it:

```
mount /mnt/cdrom
```

Then type the following commands to install INN:

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh inn-*
```

## Configuring and Starting the INN Server

Much of the InterNews (INN) software, bundled with Fedora Core, is ready to go as soon as you install the RPM. All you need is to brush up a bit on the various components of INN, edit the configuration files, and start inn—the server. By ways, I refer to the INN as the news server.

If you want to support a selection of Internet newsgroups, you also have to arrange for a news feed — the source from which your news server gets the newsgroup articles. Typically, you can get a news feed from an ISP, but the ISP charges an additional monthly fee to cover the cost of resources required to provide the feed. You need the name of the upstream server that provides the news feed, and you have to provide that server with your server's name and the newsgroups you want to receive.

Depending on the newsgroups you want to receive and the number of days you want to retain articles, you have to set aside appropriate disk space to hold the articles. The newsgroups are stored in a directory hierarchy (based on the news names) in the /var/spool/news directory of your system. If you're setting up a new server, you may devote a large disk partition to the /var/spool/news directory.

In your server's configuration files, enter the name of the server providing the news feeds. At the same time, add to the configuration files the names of downstream servers (if any) that receive feeds from your server. You can then start the new server and wait for news to arrive. Monitor the log file to ensure that the news articles are stored properly in the /var/spool/news directory over your system.

When news is up and running, you must run news maintenance and cleanup scripts by running the cron jobs. On Fedora Core, a cron job is already set up to run the /usr/bin/news.daily script to perform the news maintenance tasks.

In the following sections, I introduce you to INN setup, and you can find out more about INN from the Internet Software Consortium (ISC), a nonprofit dedicated to developing and maintaining open source software, such as BIND (implementation of Domain Name System), DHCP (Dynamic Host Configuration Protocol), and INN. Rich Salz took over the development of INN in 1996. You can find out more about INN and can access other resources at ISC's Web page at www.isc.org/products/INN.

### InterNetNews components

INN includes programs that deliver and manage newsgroups. It also includes a number of files that control how the INN works. The most important INN programs are:

- innd: The server. It runs as a daemon — a background process that keeps itself providing a specific service — and listens on the NNTP port (TCP port 119). The inn server accepts connections from other sites, as well as local newsreader clients, which hands off local connections to the nnprpd.
- nnprpd: A special server invoked by innd to handle requests from local newsreader clients.
- expire: Removes old articles based on the specifications in the text file /etc/news/expire.ctl.
- nntpsend: Invokes the innxmit program to send news articles to a remote site using NNTP. The configuration file /etc/news/nntpsend.ctl controls the nntpsend program.
- cltinnd: Enables to control the innd server interactively. The cltinnd program can send messages to the control channel of the innd server.

The other vital components of INN are the control files. Most of these files are in the /etc/news directory of Fedora Core system, although a few are in the /var/lib/news/ directory. Between those two directories, you have more than 30 INN control files. Some important files include the following:

- /etc/news/inn.conf: Specifies configuration data for the innd server. (To view online help for this file, type man inn.conf.)
- /etc/news/newsfeeds: Specifies what articles to feed downstream to other news servers. (The file is complicated, but you can get by help by typing man newsfeeds.)
- /etc/news/incoming.conf: Lists the names and addresses of hosts that provide news feeds to this server. (To view online help for this file, type man incoming.conf.)
- /etc/news/storage.conf: Specifies the storage methods to be used. (To view online help for this file, type man storage.conf.)
- /etc/news/expire.ctl: Controls expiration of articles, on the newsgroup level, if desired. (To view online help for this file, type man expire.ctl.)
- /var/lib/news/active: Lists all active newsgroups, showing the oldest and newest article for each newsgroup. (To view online help for this file, type man active.)
- /var/lib/news/newsgroups: Lists newsgroups, with a brief description of.
- /etc/news/readers.conf: Specifies hosts and users that are permitted to read news from this server. The default file allows only localhost to read news; you have to edit it if you want to allow other hosts. (To view online help for this file, type man readers.conf.)

In the next few sections, I describe how to set up some of the important files.

#### the inn.conf file

This file holds configuration data for all INN programs — which makes it the most important file. Each line of the file has the value of a parameter in the following format:

parameter: value

Depending on the parameter, the value is a string, a number, or true or false. As in many configuration files, comment lines begin with a pound sign (#).

Most of the parameters in the default inn.conf file in the /etc/news directory do not require changes. You may want to edit one or more of the parameters shown in Table 4-2.

| Table 4-2 Configuration Parameters in /etc/news/inn.conf | |
| Parameter Name | Description |
| mta | Set this parameter to the command used to start the mail agent that is used by inn to transfer messages. The default is to use sendmail. |
| organization | Set this parameter to the name of your organization in the way you want it to appear in the Organization: header of all news articles posted from your system. Users may override this parameter by defining the ORGANIZATION environment variable. |
| ovmethod | Set the type of overview method (the overview is an index of news articles in the newsgroup). The default method is tradindexed, which is fast for reading news, but slow for storing items. |
| path | Set this parameter to the name of your news server as you want it to appear in the Path header of all postings that go through your server. If path is not defined, the fully qualified domain name of your system is used. |
| pathnews | Set this parameter to the full pathname of the directory that contains INN binaries and libraries. In Fedora Core, path is set to /usr/lib/news. |
| domain | Set this parameter to the domain name for your server. |
| allownewnews | Set this parameter to true if you want INN to support the NEWNEWS command from newsreaders. In the past, this option was set to false because the NEWNEWS command used to reduce the server's performance, but nowadays the default is set to true. |

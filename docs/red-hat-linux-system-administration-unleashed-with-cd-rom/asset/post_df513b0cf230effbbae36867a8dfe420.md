
## LISTING 23.1 continued

```
maxforks: 10
maxartsize: 1000000
nicekids: 4
nicenewnews: 0
verifycancels: false
logcancelcomm: false
wanttrash: false
remembertrash: true
linecountfuzz: 0
peertimeout: 3600
clienttimeout: 600
allownewnews: true
localmaxartsize: 1000000
logartsize: true
logipaddr: true
logsitename: true
maxconnections: 50
artcutoff: 14
icdsyncount: 10
hiscachesize: 0
readertrack: false
strippostcc: false
status: 0
timer: 0
readerswhenstopped: true
noreader: false
extendeddbz: false
nmrpoverstats: false
storeonxref: true
nmrpdcheckart: true
storesmsgid: true
usecontrolchan: false
mergetogroups: false
backoffauth: false
backoffdb: /usr/local/news/db/backoff
backoffpostfast: 0L
backoffpostslow: 1L
backofftrigger: 10000L
mimeversion:
mimecontenttype:
mimeencoding:
refusecybercancels: false
```

## LISTING 23.1 continued

```
activedenable: false
activedupdate: 30
activedport: 1119
nnrperlauth: false
#
#
# These options are unlikely to need changing in most situations
#
chaninacttime: 600
chanretrytime: 300
pauseretrytime: 300
nntplinklog: false
nntpactsync: 200
badiocount: 5
blockbackoff: 120
#
# -----------------------------
# Changing these options can have an effect on the way articles are
# stored and may require recreating the spool and/or database files
#
wireformat: false
xrefslave: false
nnrpdpdhost:
nnrpdpdport: 119
spoolfirst: false
writelinks: true
storageapi: false
articlemap: false
overviewmap: true
bindaddress: all
sourceaddress: any
port: 119
#
## Keywords-in-overview options
## Enabling this without stopping inn and deleting the existing overview
## database and adding will probably confuse a lot of things. You must
## have compiled this support in too.
#
keywords: false
keylimit: 512
keyartlimit: 100000
keymaxwords: 250
```

## LISTING 23.1 continued

```
#
# Other options
innflags:
doinwatch: true
innwatchslepttime: 600
pgpverify: true
controlfailnotice: false
logcycles: 3
innwatchpauseload: 1500
innwatchhiload: 2000
innwatchloload: 1000
innwatchpoolspace: 8000
innwatchbatchspace: 800
innwatchlibspace: 25000
innwatchspoolnodes: 200
.
docnfstat: false
#
# ------------------------
# Paths to various aspects of the news system
#
pathnews: /usr/local/news
pathbin: /usr/local/news/bin
pathfilter: /usr/local/news/bin/filter
pathcontrol: /usr/local/news/bin/control
pathdb: /usr/local/news/db
pathetc: /usr/local/news/etc
pathrun: /usr/local/news/run
pathlog: /usr/local/news/log
pathhttp: /usr/local/news/log
pathtmp: /usr/local/news/tmp
pathspool: /usr/local/news/spool
patharticles: /usr/local/news/spool/articles
pathoverview: /usr/local/news/spool/overview
pathoutgoing: /usr/local/news/spool/outgoing
pathincoming: /usr/local/news/spool/incoming
patharchive: /usr/local/news/spool/archive
pathuniover: /usr/local/news/spool/uniover
overviewname: .overview
#
# ------------------------
```

It's not a small file, and that's testament to how complex a system we're dealing with here. Keep in mind that there are many config files also.

Table 23.1 shows some of the parameters in the file. You don't need to change all of them because the defaults will usually work.

## TABLE 23.1 inn.conf Parameters

| Parameter | Explanation |
|---|---|
| Organization | Set to the name of your organization as you want it to appear in the Organization: header of all local posts. This will be overridden by the value of the ORGANIZATION environment variable (if it exists). If neither this parameter nor the environment variable are set, no Organization: header will be added. |
| Pathhost | This is the name of your news server as you want it to appear in the Path header of all postings that travel through your server (this includes local posts and incoming posts that you forward out to other sites). If no pathhost is specified, the FQDN of the machine will be used instead. |
| Domain | Sets the domain name for your server. This is normally determined automatically by INN, but in some cases it is necessary to set it manually. For example, if you are running NIS on a SunOS system and your hostnames are not fully qualified (that is, your systems are named xxxx instead of xxxx.domain.com), you will need to use this option to set your domain name manually. If in doubt, leave this option commented out or remove it completely. |
| maxartsize | This is the maximum size of articles this server will accept through a newsfeed. Articles larger than this size will be rejected. GOTCHA: You might think that decreasing this setting will prevent large articles from hogging your bandwidth. However, all it will do is make the server throw articles larger than this size away after it's completed downloading them. It's not a bad idea to lower this parameter to keep large articles from taking up space. |
| complaints | If present, this address is used to add an X-Complaints-To: header to all local posts. The usual value would be something like abuse@your.domain or postmaster@your.domain. If not specified, the news master email address will be used. |
| allownewnews | If set to true, INN will support the NEWNEWS command for news readers. This will really kill your server performance and it is strongly suggested that you set this to false. GOTCHA: The default is true. Change it. I don't know why it's distributed this way, but it's not a good idea. |

## Table 23.1 continued

| Parameter | Explanation |
|---|---|
| localmaxartsize | This is the maximum allowed size of locally posted articles. Articles larger than this size will be rejected. GOTCHA: Unless you'll be making large posts to local newsgroups (not distributed to Usenet at large), the default parameter is too big. Large files should be made available through http or ftp access, and a link posted to Usenet. Change it. A reasonable size is 50,000-100,000 bytes. |
| status timer | Determines how often status and timer updates are written to the log files. The value is specified in seconds with a value of 0 disabling logging. The suggested value is 300 seconds (5 minutes). |
| storageapi | Set to yes if articles should be stored using the Storage Manager API. You must set this to no if you are using the traditional article storage method or yes if you are using timhash or CNFS. See the section "Choosing an Article Storage Format" for more information. |
| extendeddbz | This is only used if you did not configure INN for tagged hash and you are using the storage API. If set to yes, overview offset information for articles is stored in the DBZ history hash file as well as in the history text file. This will make the hash file three times larger, but should increase performance for news readers when they retrieve article overview information. If you don't mind using 200-300MB of extra space for your history database and memory, you should set this to yes. |
| nnrpd overstats | If set to yes, nnrpd will log statistics about how much time was spent during the various stages of reading article overview information. Not terribly useful unless you are trying to track down news reader performance problems. |
| hiscachesize | The size in kilobytes to use for caching recently used history file entries. Setting this to 0 disables history caching. History caching can greatly increase the number of articles per second that your server is capable of processing. A value of 16384 (16MB) is a good choice if you can spare the RAM. |
| overviewmap | Overview data is mmaped and reading overview would be faster with this. |

## Table 23.1 continued

| Parameter | Explanation |
|---|---|
| usecontrolchan | All control messages, except cancels, will be processed in batch mode by controlchan. Otherwise, they will be processed one-by-one with forked processes from innd. To reduce excessive load when many control messages arrive in a short time, this is useful and recommended. Controlchan will log its error to syslog, if Sys::Syslog is available. Otherwise it logs to errlog. To enable Sys::Syslog, you need to do following: # cd /usr/include # h2ph * # cd /usr/include/sys # h2ph * GOTCHA: Again, this is by default not configured the recommended way. Change it. And, enabling syslog as above is a good idea too. |

These are just some parameters you should look over. If you want a complete description, look in the man page for inn.conf. You can read the man page with this command:

```
man /usr/local/news/man/man5/inn.conf.5
```

## Note

If /usr/local/news/man is in your MANPATH, you can just do man inn.conf. This is an exercise left to the reader. (I hated when my professors said that, so I take a certain pleasure in saying it to you.)

## newsfeeds

The newsfeeds file determines how incoming articles are redistributed to your peers and to other INN processes. The newsfeeds file is very versatile and contains dozens of options; we will touch on just the basics here. The newsfeeds man page contains more detailed information.

The newsfeeds file is organized as a series of feed entries. Each feed entry is composed of four fields separated by colons. Entries may span multiple lines by using the backslash (\ ) to indicate that the next line is a continuation of the current line.

```
my-feed-site.domain.com/exclude-list\
:newsgroup-list\
:Tm:innfeed!
```

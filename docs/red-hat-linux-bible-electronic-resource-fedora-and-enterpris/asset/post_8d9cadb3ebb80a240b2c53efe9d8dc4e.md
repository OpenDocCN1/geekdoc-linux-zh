
innwatchloload and innwatchhioload set the range of load average, which causes the INN server daemon to be throttled. The following lines contain the default parameters that relate to monitoring:

```
do_innwatch:            false
innwatchbatchspace:    800
innwatchlibspace:      25000
innwatchloload:        1000
innwatchhioload:       2000
```

For other parameters related to monitoring INN resources, refer to the inn.conf man page.

## Logging parameters

Several parameters in the inn.conf file can be used to change what information is logged and how it is logged. News log information is written to log files in a directory set by the pathlog parameter. By default, the pathlog parameter is set to /var/log/news.

- The docnfsstat parameter lets you turn on or off the cnfsstat program. Cnfsstat monitors the usage of cycbuffs if you are using the Cyclic News File System to store your news articles. The parameter is off (false) by default.

```
docnfsstat:             false
```

- To have the size of an article written to the log file, set the logartsizer parameter to true. By default, logartsizer is on, as follows:

```
logartsizer:            true
```

- Use the logcancelcomm parameter to log ctlinnd cancel commands to syslog. This parameter is off by default, as follows:

```
logcancelcomm:          false
```

- To set the number of logs that news.daily keeps before it overwrites them, set the logcycles parameter. By default, this number is set to 3, as follows:

```
logcycles 3
```

- Use the logipaddr parameter to have the IP address of the host logged for a received article. By default, this is on, as follows:

```
logipaddr:              true
```

- If you want the site names for received articles to be put in the article log file, the logsitename parameter should be on. By default, it is on, as follows:

```
logsitename:            true
```

- To have overview statistics related to the nnrpd daemon process logged to syslog, turn on the nnpdoverstats parameters. By default, this parameter is off, as follows:

```
nnpdoverstats:      false
```

- The nntpactsync parameter sets the number of articles that can come on an incoming channel before the activity is logged. The default value is 200 articles, as follows:

```
nntpactsync:       200
```

- The ntplinklog parameter indicates whether or not to place accepted articles' storage API token. By default, this parameter is not on (false).

```
ntplinklog:        false
```

- To enable status monitoring, you need to turn on the status parameter by setting the value to a number. By default, this parameter is off (0). To have it turned on, set the value to the number of seconds between which status monitoring statistics are logged. You could set the value to 600 seconds as follows:

```
status:            600
```

- To enable performance monitoring, you need to turn on the timer parameter. By default, timer is off (0). To have it turned on, set the value to the number of seconds between which performance statistics are logged. You could set the value to 600 seconds as follows:

```
timer:             600
```

## System tuning parameters

A set of low-level tuning parameters is available for tuning your INN server. In most cases, you shouldn't need to change these parameters. These parameters include: badiocount, blockbackoff, chaninacttime, chanretrytime, icsdyncount, maxforks, nicekids, nicenewnews, nicenrpd, pauseretrytime, peertimeout, and rlimitnofile. If you are interested in learning more about the INN system tuning parameters, refer to the `inn.conf` man page.

## News directory parameters

The `inn.conf` file sets the location of directories that contain newsgroup information. Although you shouldn't have a need to change these locations, knowing where they are can be useful. The following text is taken from the `inn.conf` file, to show where the different news directories are located:

```
patharchive:       /var/spool/news/archive
patharticles:      /var/spool/news/articles
pathbin:           /usr/lib/news/bin
pathcontrol:	/usr/lib/news/bin/control
pathdb:	/var/lib/news
pathetc:	/etc/news
pathfilter:	/usr/lib/news/bin/filter
pathhttp:	/var/log/news
pathincoming:	/var/spool/news/incoming
pathlog:	/var/log/news
pathoutgoing:	/var/spool/news/outgoing
pathoverview:	/var/spool/news/overview
pathrun:	/var/run/news
pathspool:	/var/spool/news
pathtmp:	/var/lib/news/tmp
```

## Setting Up News Feeds

For the flow of news articles to take place, news servers need to know about each other and need to be willing to exchange articles. The `/etc/news/incoming.conf` file lists the host computers that you allow to connect to feed your news. You use the `/etc/news/newsfeeds` file to set up where your news articles should be sent. You have to set up both of these files.

## Configuring hosts to feed you

To configure the host computers that feed articles to your news server, you need to configure the `/etc/news/incoming.conf` file. In this file, you can set various key/value parameters that affect how these news feeds behave. Other entries are either peer entries or group entries. The key/value entries set values that are assigned to every peer and group entry. Those values can be overridden for particular peers or groups by adding new key/value entries within peer and group entries. Peer entries identify the fully-qualified domain name (FQDN) of a computer that can feed news to your server, along with any key/value entries. Group entries are a way of assigning groups of peers to have particular key/value entries.

The whole thing seems a bit complicated when all you are doing is defining which hosts can send news to you and how they are allowed to do that. Here is an example of the contents of an `incoming.conf` file from its man page:

```
max-connections:	5	# per feed

# A peer definition.
peer usenet {
	hostname: usenet1.uu.net
}

peer vixie {
	hostname: gw.home.vix.com
	max-connections: 10 # override global value.
}

# A group of two peers who can open more
# connections than normal
group fast-sites {
    max-connections: 15

    # Another peer. The ``max-connections'' value from the
    # ``fast-sites'' group scope is used. The hostname value
    # defaults to the peer's name.
    peer data.ramona.vix.com {
    }

    peer bb.home.vix.com {
        hostname: bb.home.vix.com
        max-connections: 20 # he can really cook.
    }
}
```

The only key/value pair in this example is `max-connections: 5`, which defines the maximum number of connections from any one host to be five (unless overridden in a peer or group value). Two individual hosts are defined as news feeders: usenet (`usenet1.uu.net`) and vixie (`gw.home.vix.com`). The vixie definition is an example of using a key/value pair to override a default value.

The group example is just a way to set key/value entries for several hosts at the same time. This example sets the maximum number of connections to 15 and assigns that value to all the peers in the group (`data.ramona.vix.com` and `bb.home.vix.com`). Then, as an illustration, the value is overridden for the second of those hosts by setting the value to 20.

The host name can be a full host.domain name or an IP address. As you have already seen, `max-connections` can set the maximum number of connections that are enabled at a time from a host (0 enables unlimited connections). Here are some key/values that you can set globally, for a particular peer, or within a group:

- **hostname:** Identifies the host.domain name or IP address of the news server.
- **streaming:** Defines whether streaming commands are enabled (`true` or `false`).
- **password:** Assigns a string to this key that must be used by the host as a password before it can connect. By default, no password is required.
- **noresendid:** Causes the `innd` daemon to send a `431 RESENDID` response to an article that has already been received from another peer.

## Configuring hosts that you feed

The entries that you place in the `/etc/news/newsfeeds` file define how the articles that your news server receives are fed to other news servers. This file offers a lot of opportunity for configuration. The main reason this file is so complex is that it enables you to select which


specifies the domain and other global data, such as the working directory of the named. In addition, the names of the underlying files are determined.

After the change in the database, the named must re-read the data. For this purpose, you can send the daemon SIGHUP signal (for example with kill -HUP 'cat /var/run/named.pid') or you can use the named.reload script. With the named.restart script, the daemon can be terminated and restarted. For simple server management, you can also use the ndc program installed.

Another important signal is SIGINT, which causes the daemon to output its database in the file /var/tmp/named_dump.db. This is sometimes necessary for debugging. Several other signals exist to control the daemon; they are documented in the man page.

## 20.4 Global configuration

BIND8 is much more flexible than previous versions in terms of general configuration. You may add comments to the file in the form of Perl, C++, or C comments (starting with # or // to the end of line or enclosed in /* */). All other entries must be valid statements: the most useful are presented here. See the man page details.

- logging
Specifies what messages the server logs via syslog or into a file, and where the log messages are sent. This statement may only occur once in the configuration file.

- options
Controls global server configuration options and sets defaults for other statements. This statement too may occur once.

- zone
Defines a zone. A name server may serve several zones, so it may occur often. We will discuss the different kinds of zones in the following sections.

- acl
Defines a named IP address matching list, for access control and other uses.

### 20.4.1 Logging

The output of logging goes to different channels. A channel may be a file, a syslog facility, specify an internal descriptor such as stderr, or the sink null. Once a channel has been defined, it cannot be redefined.

The input for the logging system comes from different categories. You can specify to which channel all these messages will be logged. Listing 20.2 is an example of a simple logging scheme that logs all queries via syslogs daemon.info. Beside that it defines a file channel called lamers. The file will grow up to 20 Mbytes and three versions will be kept. For more details, see the man page.

```
Logging (
    channel query {
        syslog daemon;
        severity info;
    }
    channel lamers {
        file "lamers.log" versions 3 size 20m;
        print-time yes;
        print-category yes;
    }
    category queries {
        channel query;
    }
);
```
**Listing 20.2** Excerpt from named.conf: logging configuration.

If you find yourself reading too many log messages, you may send more categories to the null channel. If you want more output, define a new channel (probably a file channel) and redirect the category to that channel.

### 20.4.2 General options

For most systems, you won't need many general options. In any case you will find a complete list with descriptions in the man page named.conf. Listing 20.3 presents a simple configuration used on my system. All data are stored in the directory /etc/named as long as the filenames are specified as a relative path. All queries that can't be answered locally are forwarded to the name server of my provider and finally I check that names are correct.

## 482 CONFIGURATION AND OPERATION OF A NAME SERVER

```
options {
    directory "/etc/named";
    forwarders {
        194.45.71.65;
        194.45.71.65;
        194.45.71.65;
    };
    check-names master fail;
    check-names slave warn;
    #-default ignore
    check-names response warn;
}
```
Listing 20.3 General options for named.

BIND has been written for large servers, so the administrator can change as many parameters as he/she likes. If you run a name server for more than one or two local zones, you will eventually need to read the man page and change a couple of parameters. On the other hand, most simple installations will not need many changes to be made.

## 20.5 Primary name servers

There are a number of name server types. In each zone, there must be one primary server which manages the authoritative data for that zone. For reasons of safety against failures, at least one name server should exist which is operated as a secondary server. The required configuration for a secondary server can be found in Section 20.10. For computers that are only temporarily connected to the Internet, for example via SLIP or PPP, it might be sensible to set up a caching-only name server.

The operation of a name server requires additional computing power and memory on the corresponding computer together with a greater administrative effort in comparison with simple editing of the file /etc/hosts. Essentials, there are two (compelling) reasons for installing your own name server:

- You apply for a new domain. Talk to your provider about who will be operating the name server for this domain. If you want to operate the name server yourself, your provider must configure his site accordingly. Often, your provider will initially operate the name server for you.

## PRIMARY NAME SERVERS 483

- You want to set up new name server for an organizational zone inside an already existing domain. You must discuss this with your network administrator, otherwise your new server will not be recognized as authorized.

Your own name server, however, also has its advantages, no matter whether you are connected to the Internet or not:

- In a local network, all computer names are always known on all other computers.

- The database is always up to date and consistent on all computers. The hosts files otherwise needed on the different computers tend to become obsolete and possibly contradictory fairly quickly.

- Assignment of name and IP addresses is consistent.

- If you operate the name server yourself, you can change data without having to bring in your provider.

Listing 20.4 shows an example of the file /etc/named.conf on a primary name server. directory specifies the directory in the files of this name server are stored. A computer can be the primary and/or secondary server for several zones. The only requirements are that the primary lines are entered in the file /etc/named.conf and the corresponding data is available.

Each name server should create cache of requests and answers. This can be done by means of the keyword cache. At the start of the name server, all data from named.root that is still correct is reloaded into the cache. A name server becomes a cache-only server if no zone of the type master or slave is contained in the file named.boot.

The name server must know where to find the authoritative name server for the root domain of the network. This information is stored in the file named.root. In many documents, this file is also called root.cache, although this does not describe its purpose. The name of the file is specified in the zone type hint.

## 484 CONFIGURATION AND OPERATION OF A NAME SERVER

```
# host file excerpt for name server
options {
    directory "/etc/named";
}
# Rest Name-Server
zone "" {
    type hint;
    file "local.cache";
}
zone "example.org" {
    type master;
    file "named.hosts";
}
zone "0.0.0.127.in-addr.arpa {
    type master;
    file "named.local";
}
zone "192.192.168.in-addr.arpa" {
    type master;
    file "named.rev";
}
```
Listing 20.4 The file .etc/named.conf for a primary name server.

This file, like all other data files, is stored in standard Resource Record (RR) or Masterfile format. A detailed description of this format can be found in the BIND Operators Guide; an introduction is given in the following paragraphs.

The name server is a primary name server for the zone veggies.example.org. The database is located in the file named.hosts in the directory /var/named. In addition, the server is a primary name server for the zones 0.0.127.in-addr.arpa and 168.192.in-addr.arpa, which are used for 'reverse lookup'.

In the next step, the data of the individual computers whose zones are specified in the file /etc/named.conf must be entered in the corresponding files. The format of these files and the most important entries are explained in more detail on the following pages.

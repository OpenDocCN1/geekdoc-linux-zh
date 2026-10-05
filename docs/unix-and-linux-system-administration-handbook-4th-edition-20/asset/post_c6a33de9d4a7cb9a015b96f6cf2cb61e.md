
# Chapter 17 DNS: The Domain Name System

## Version determination

It often doesn't seem to occur to vendors to document which version of an software package they have included with their systems, so you might have to do some sleuthing to find out exactly what software you are dealing with. You can sometimes determine the version number with a sneaky dig, a command that comes with BIND.

```
$ dig @server version.bind txt chao
```

returns the version number unless someone has decided to withhold information by changing it in BIND's configuration file. First, determine the name of the name server for the domain in question with

```
$ domain ns
```

and then do query the version.bind query. For example, the command works at isrc:

```
$ dig @ns-ext.isc.org version.bind txt chao
version.bind 0 CH TXT "9.5.1"
```

But it doesn't work at cs.colorado.edu:

```
$ dig @mroe.cs.colorado.edu version.bind txt chao
version.bind 0 CH TXT "wouldn't you like to know..."
```

Some sites configure BIND to conceal its version number on the theory that this provides some degree of "security through obscurity." We don't endorse this practice, but it might help fend off some the script kiddies. See page 603 for a more detailed description of this topic.

This sample query works for other DNS software; for example,

```
$ dig @root-servers.net version.bind txt chao
version.bind 0 CH TXT "NSD 2.3.7"
```

shows that the K root name server is running,

Another piece of data in the CHAOS class identifies the name of the server query. But—if you just queried the server, you must know its name, right? Actually of the busiest servers (e.g., the root name servers) are really multiple machines scattered around the globe that have the same server name and IP address. This replication scheme is called "anycast routing." The routing system takes you to the "closest" instance. If you are the sysadmin trying to debug a problem, however, it might be important to distinguish which of the replicated servers you have reached. For example,

```
$ dig @root-servers.net hostname.bind txt chao
hostname.bind 0 CH TXT "k2.nap.k.ripe.net"
```

> 17. The 0 in the answer is for the data value. One of our reporters noticed seeing to this query comes as "Name as Bind, James Bind!"

or

```
$ dig @k.root-servers.net id.server txt chaos
id.server.    0 CH TXT "k2.nap.k.ripe.net"
```

The IETF tried to standardize these odd CHAOS-class names into independent-dense forms, version.server and id.server, but only id.server made it through the process; version.server ended up in an IETF draft that became an RFC. NSD uses all four forms, but only the three approved forms.

As an administrator, you can start the server name (named nsd) with the -v flag to print its version to standard output and exit. On Linux, you can ask your package manager which version is installed. You can also tell what BIND version by inspecting the log files in /var/log or its equivalent to your system. The BIND server name logs its version to syslog (daemon) as it starts up. grep for BIND to get lines like:

```
Jul 13 07:19:55 nubark named[757]: starting BIND 9.5.0-P2 -u named
```

If all else fails, dig's version number usually parallels named's, and dig is often installed even when named is not. dig's first line of output includes the version number as a comment.

Table 17.8 shows the versions of BIND that are included with our example systems. It's always safe to use the current release.

## 17.8 Versions of BIND shipped with our example systems

| System | OS vers | BIND vers | BIND release date |
| :--- | :--- | :--- | :--- |
| ISC | | 9.6.1-P3 | January, 2010 |
| Ubuntu | 9.04 | 9.5.1-P2 | March, 2009 |
| SUSE | 10.2 | 9.4.2 | November, 2007 |
| RHEL | 5.3 | 9.3.4-P1 | July, 2007 |
| Solaris | 5.10 | 9.3.4-P1 | July, 2007 |
| OpenSolar | 2009.06 | 9.6.1-P1 | July, 2007 |
| HP-UX | 11 | 9.3.2 | December, 2005 |
| AIX | 6.1 | 8.3.3 or 9.2.1 | January, 2004 |

AIX ships back-port security fixes to their installed version of an older release rather than upgrade to the latest release from ISC, so version numbers can be deceiving. As you see, many of the vendors are not current, so your sysadmin might be to upgrade the software. AIX ships both BIND 8 and BIND 9, respectively. The generic form is linked to named. The + in the version number is for not exactly. See Chapter 11 for more information about syslog.

Each statement begins with a keyword that identifies the type of statement. There can be more than one instance of each type of statement, except for options and logging. Statements and parts of statements can also be left out, invoking default.

Before describing these statements and the way they are used to configure **named**, we need to describe a data structure that is used in many of the statements, the address match list. An address match list is a generalization of an IP address that can include the following items:

- An IP address, either v4 or v6 (e.g., 199.165.144)
- An IP network specified with a CIDR netmask (e.g., 199.165.16/15)
- The name of a previously defined access control list (see page 609)
- The name of a cryptographic authentication key
- The ! character to negate things

Address match lists are used as parameters to many statements and options.

```
{ 1.2.3.13; 1.2.3/24; \
128.138.16/24; 198.11.16/24; 204.228.69/24; 127.0.0.1; };
```

The first of these excludes the 1.2.3.13 but includes the rest of the 1.2.0/24 network; the second defines the networks assigned to the University of Colorado. The braces and final semicolon are not really part of the address match lists but are included for illustration; they would be part of the enclosing statement of which the address match lists are a part.

When an IP address or network is compared to a match list, the list is searched in order until a match is found. This "first match" algorithm makes the ordering of entries important. For example, the first address match list above would have the desired effect if the two entries were reversed, because 1.2.3.13 would succeed in matching 1.2.3.0/24 and the negated entry would not be encountered.

Now, on to the statements! Some are short and sweet; others almost warrant a chapter unto themselves.

## The include statement

Break up or organize a large configuration, you can put different portions of the configuration in separate files. Subsidiary files are brought into named.conf with an include statement:

```
include "path";
```

If the path is relative, it is interpreted relative to the directory specified in the directory option. A common use of the include statement is to bring in keys that would not be world-readable. Rather than doing closing access to the whole named.conf file, some sites keep keys in restricted permissions that named can read. Those files are included into named.conf.

Many sites put zone statements in a separate file and use the include statement to pull them in. This configuration helps separate the parts of the configuration that are relatively static from those that are likely to change.

## The options statement

The options statement specifies global options, some of which may be overridden for particular zones or servers. The general format is

```
options {
  option;
  option;
  ...
```

If no options statement is present in named.conf, default values are used.

BIND has a lot of options—too many, in fact. The 9.7 release has more than 150, which is a lot for sysadmins to wrap their heads around. Unfortunately, as soon as the BIND think about removing some of the options were a bad idea or that are no longer necessary, they get pushback from sites who use and need obscure options. We do not cover the gamut of BIND options here; we have biased our coverage and discuss only the ones whose we recommend. We also asked the BIND developers for their suggestions on options to cover, and followed their advice.

For more complete coverage of the options, see one of the books on DNS and BIND listed at the end of this chapter. You can also refer to the documentation shipped with BIND. The ARM document in the doc directory of the distribution

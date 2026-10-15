

The server-count option specifies the number of instances of nsd to start. For multi-CPU machines, you may want to increase this value. xfrd-reload-timeout throttles reloads after zone transfers by waiting at least the specified number of seconds since the last reload before reloading again.

Security
username: login [nsd]
chroot: directory [none]

nsd must start running as root in order to open a privileged socket (port 53), but it can then drop back to the privileges of a normal user as long as all the files it needs are owned by that user. Hence, the dedicated nsd account.

For added security, you can also run nsd in a chrooted jail as long as the zone files, database file, xfrdfile, diff file, PID file, and syslog socket (or log file) are accessible through the jail directory.

## NSD zone-specific configuration options

Unlike global options, zone-specific options do generally require some configuration, especially the access control lists.

Zone definitions
name: zonename
zonefile: filename

A zone is defined by a zone name and a file of resource records.

Master ACLs
notify: ip-address { key-name | NOKEY }²³
provide-xfr: ip-spec { key-name | NOKEY | BLOCKED }²³

The master server for a zone notifies its slaves of updates to the zone. Then, when requested by the slaves, it initiates zone transfers to transmit the modified data. Therefore, a zone for which this server is the master must have the notify and provide-xfr access lists specified. The values of these options will normally be the same. Notification messages are signed with the listed key-name unless you specify the NOKEY option.

opposed to incremental updates) will be requested. The UDP argument specifies that the request for a zone transfer be sent with UDP transport rather than the default TCP. It’s best just to use TCP.

Source IP address

outgoing-interface: ip-spec

This list controls the IP address used by a slave server to request a zone transfer or by a master to send notifications. The addresses must match; that is, the access control clause in the master’s zone configuration must use the same address as the corresponding clause in the slave’s zone configuration.

## Running nsd

Once you have configured nsd, run the nsd-checkconf program to be sure there are no syntax errors in your nsd.conf file. Then put your zone files in the right directory (the one specified in nsd.conf) and use nsd, the NSD control script, to compile them into database files. Finally start the name server with nsd.

```
$ sudo nsd rebuild
$ sudo nsd start
```

Test the name server with dig or drill, and if you’re happy with the results, add nsd start to your operating system’s startup sequence and nsd stop to its shutdown sequence. You can also set up a cron tab job to run nsd patch once a day to update the text zone files from the database files.

## Installing and configuring Unbound

Unbound is a recursive, caching, validating DNS name server from the same folks (NLnet Labs) that produce NSD. It was originally developed for UNIX and Linux, but it’s now is available for Windows, too.

To install, create a new user called “unbound”, log in as this user, and download the distribution from unbound.net. Unbound requires the ldns and OpenSSL libraries and can use the libevent libraries (monkey.org/~provos/libevent) as well if they are available. Like NSD, Unbound initially runs as root, but then falls back to running under its dedicated user account.

To build:

```
$ ./configure
$ make
$ sudo make install
```

Unbound also comes with an extensive test suite that you can run with make test. The distribution installs the following binaries:

+   - unbound – the recursive name server
+   - unbound-checkconf – syntax checker of the unbound.conf file
+   - unbound-control, unbound-control-setup – secure remote control
+   - unbound-host – simple query tool

unbound-host is not as verbose as dig or drill, but it's handy for command-line validation when DNSSEC is tested.

Table 17.11 shows the locations of Unbound components.

## Table 17.11 Unbound installation directories

| Item | Directory |
|---|---|
| Binaries | /usr/local/sbin |
| Libraries | /usr/local/lib |
| Configuration file | /usr/local/etc/unbound/unbound.conf |
| Man pages | /usr/local/share |
| Secure jail | /usr/local/etc/unbound |
| PID file | /usr/local/etc/unbound |

unbound's configuration file, unbound.conf, is similar to that of nsd. The basic syntax is

```
attribute: value
```

with comments initiated by # and lasting until the end of the line. You can run unbound-checkconf to check the validity of your config file.

Here is a small example of an unbound.conf file, adapted from the man page with saner paths and some additional comments:

```
server:
  directory: "/var/unbound/etc"
  username: unbound
  chroot: "/var/unbound"
  pidfile: "/var/run/unbound.pid"

root-hints: "root.cache"
  interface: 0.0.0.0        # Listen on all IPv4 interfaces
  interface: ::0           # And on all IPv6 interfaces
  access-control: 10.0.0.0/8 allow   # Local private networks
  access-control: 2001:DB8::/64 allow # Local IPv6 networks
```

This example listens on all interfaces and allows queries from the local IPv6 networks and from the unrouted private net 10. It logs to syslog with facility daemon (the default) and runs in a chrooted jail as user unbound.

With recursion come lots of options; the unbound option list approaches half the size (70+) of BIND's (150+). Our coverage is selective. See the man page and the how-to documents at unbound.net for the full story.

unbound's config language has four top-level clauses: server, remote-control, stub-zone, and forward-zone. Global options appear beneath the server clause. Here are a few of the more important ones.


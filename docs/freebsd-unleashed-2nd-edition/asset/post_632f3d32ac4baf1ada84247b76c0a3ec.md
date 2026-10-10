
## Identifying Name Server Components

What programs are involved in name server operations and where will you be making your configuration changes:

- `/usr/sbin/named`—The name server daemon itself. It listens on port 53 for DNS lookup requests.
- `/usr/sbin/ndc`—The name daemon controller program. This is the tool you will use to start, stop, reload, and monitor the `named` server.
- `/etc/namedb`—All your BIND configuration and runtime status files, including zone definition files, are in this directory (or any subdirectories of it that you create).
- `/etc/namedb/named.conf`—The master BIND configuration file. This file tells BIND which domains you are to manage as well as how to handle each one.

## Enabling the Name Server Daemon

Enabling BIND in FreeBSD is the simplest part of configuring it. All you have to do, just as with other built-in FreeBSD services we have discussed, is add the following line to `/etc/rc.conf`:

```
named_enable="YES"
```

With this option set, `named` will run automatically at boot time. To start it without rebooting, use the `ndc` tool:

```
# ndc start
new pid is 12717
```

The server should now be running. However, this is only scratching the surface of a complete BIND configuration.

> **NOTE**
> For maximum efficiency, put a nameserver line into your `/etc/resolv.conf` file, referring to the loopback address (`127.0.0.1`) as your primary name server. This way, you will be able to perform DNS lookups the quickest way of all: from your own machine. Make sure this line appears before any additional servers:
> ```
> search somewhere.com
> nameserver 127.0.0.1
> nameserver 64.41.131.167
> ```

## Running BIND in a Sandbox

As you saw in Chapter 26, "Configuring an FTP Server," it’s sometimes advisable (for security purposes) to run certain services within what’s known as a *sandbox*, or a directory structure that's been pruned off so as to appear that it's all that exists in the filesystem. In FTP, this is known as a chroot jail; the effective “root” of the filesystem is changed so that the server and the processes it creates cannot see outside their own directory structure above a certain point. BIND provides the same kind of capability, although most of the documentation refers to it as a “sandbox” rather than as a “chroot jail.” The concept is the same, however.

A common sandbox configuration is to have a directory called sandbox within /etc/namedb, with named pruning itself off into that directory as soon as it is started. This ensures that if named is compromised (which is possible because vulnerabilities continue to be found in versions of BIND to this day), the damage is restricted to that directory. Create the /etc/namedb/sandbox directory and then change its ownership and permissions to the unprivileged bind user and group:

```
# chown -R bind:bind /etc/namedb/sandbox
# chmod -R 750 /etc/namedb/sandbox
```

Next, create /etc and /var/run subdirectories inside the sandbox. Copy /etc/localtime into /etc/namedb/sandbox/etc. The server will write runtime files into /var/run, and it needs the localtime file to process the serial numbers found in zone files and to log dates properly:

```
# mkdir /etc/namedb/sandbox/etc
# cp /etc/localtime /etc/namedb/sandbox/etc
# mkdir -p /etc/namedb/sandbox/var/run
```

Finally, add the following line to /etc/rc.conf:

```
named_flags="-u bind -g bind -t /etc/namedb/sandbox"
```

Note that when using the ndc program to control named (as you will see in this chapter), you must use the -c option if you're running named in a sandbox. The syntax would take the following form:

```
# ndc -c /etc/namedb/sandbox/var/run/ndc start
```

Also note that if you configure named to log to a file, the file must be inside the sandbox for named to be able to write to it.

## Working with the BIND Configuration File (named.conf)

In order to make your name server do anything useful, you need to make sure that it is topologically in the right place with respect to its clients and the rest of the network and that it is configured to interoperate properly with other name servers. A misconfigured name server can result in deluges of DNS traffic between your server and the root servers as it tries futilely to synchronize its data. Your /etc/namedb/named.conf file must be constructed properly, so it needs to be understood properly.

> **CAUTION**
> As should be a habit by now, be sure to make a backup copy of your `named.conf` file (such as `named.conf.bak`) before you make any changes to it. Always leave yourself the option to revert to your previous working configuration!

Fortunately, BIND 8 (the version included in FreeBSD at the time of this writing, probably soon to be replaced with BIND 9, which can be installed from the ports) greatly simplifies many of the esoteric details of name server configuration that were the norm in BIND version 4 and earlier. BIND 8, which immediately replaced BIND 4, introduced a lot more configurability and at the same time eliminated many elements that were obsolete or poorly designed. Listing 31.1 shows a sample `named.conf` file, giving you an idea of its syntax and structure.

```
LISTING 31.1 Sample `/etc/namedb/named.conf` File
/*
 * A simple BIND 8 configuration
 */

logging {
	category lame-servers { null; };
	category cname { null; };
};

options {
	directory "/etc/namedb";
};

zone "somewhere.com" {
	type master;
	file "somewhere.com";
};

zone "131.41.64.in-addr.arpa" {
	type master;
	file "131.41.64.in-addr.arpa";
};

zone "elsewhere.com" {
	type slave;
	file "slave/elsewhere.com";
	masters { 113.125.2.145; };
};
```

```
LISTING 31.1 Continued

zone " ." {
type hint;
file "named.boot";
};

zone "0.0.127.in-addr.arpa" {
type master;
file "localhost.rev";
};

zone "0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.IP6.INT" {
type master;
file "localhost.rev";
};
```

As shown in the listing, a configuration file consists of a number of blocks (or *statements*) in C-style syntax, with substatements allowed within curly brackets (`{}`) . All possible statements are listed and described in the *man named.conf* page. Some of the most useful ones are options, controls, logging, and zone.

Comments in *named.conf* are also C style; single-line comments are done with double slashes (`//`) , and block comments are done with the `/* comment */` syntax. Shell-style comments (`#`) are also supported.

The *named.conf* file that exists in the default installation of FreeBSD has a few of the statements shown in Listing 31.1 and a few that are not. It also has a lot of inline documentation that describes how to use each of them.

Whenever you make a change to *named.conf* or to any of the zone files (which we will discuss later in this chapter), restart *named* using the *ndc* program:

```
# ndc reload
Reload initiated.
```

## Using a Forwarder

Recalling the topology shown in Figure 31.1, a *forwarder* is a name server at an “upstream” network—a larger network “closer” to the root servers—that allows you to request DNS information from it. (Note that access to a name server can be restricted, as you will see.) A good candidate for a forwarder is your uplink ISP’s name server, if your FreeBSD machine is acting as a name server for a home network. Normally, if your machine can't answer a DNS request on its own, it must query the root servers (found in `/etc/namedb/named.root`) for the authoritative reply. These extra steps take time and add to the packet traffic on the network.

It really isn't necessary for everyone to get authoritative answers all the time. It's perfectly acceptable in most cases to work from nonauthoritative DNS information, such as that from a caching name server:

```
# nslookup www.freebsd.org ns.somewhere.com
Server:    ns.somewhere.com
Address:   64.41.131.172

Non-authoritative answer:
Name:      freefall.freebsd.org
Address:   216.136.204.21
Aliases:   www.freebsd.org
```

Configuring your FreeBSD system to query one or more forwarders allows it to benefit from the cache of the upstream name server, rather than to fetch authoritative data on every query. The downside (as we discussed earlier) is that the cached data can become "stale" by as much time as the authoritative server's zone file specifies it should (a period frequently measured in days—though most forwarders do use reasonably short TTL values, which mitigates this drawback). Figure 31.2 shows a DNS query path in which a forwarder is involved. The forwarder does most of the work, building up its cache through queries of its own and in service to its own clients. The downstream DNS that points to it needs only to query the forwarder, thus preventing unnecessary lag and query traffic.

> **TIP**
> The deluges of DNS traffic mentioned earlier are often caused by name servers that are improperly configured, never to take advantage of caching name servers. These forwarders are what prevent too much unnecessary traffic from swamp-ing low-bandwidth links—for instance, in cases where a DNS host serving as the authoritative name server for a domain is on a small DSL or dial-up link. Without caching name servers, every host on the Internet would have to send DNS queries to that overloaded name server directly. With forwarders, the load on the target host's link is greatly reduced. Using a forwarder is a way to act as a good network citizen and make your own queries faster and more efficient.

To enable a forwarder, replace 127.0.0.1 in the forwarders block of the options statement with the upstream name server's IP address (127.0.0.1, the localhost address, will not work here) and uncomment the block by removing the `/*` and `*/` comment tags:

```
/*
    forwarders {
        127.0.0.1;
        66.114.72.112;
    };
*/
```

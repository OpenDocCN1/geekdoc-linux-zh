
www.bertjwregeer.com, though, the resolver doesn’t add the default domain.

Maybe I have more than one domain I’d like to search. Use the *search* keyword to give a list of domain names to try, in order. Like *domain*, *search* must be the first line of *resolv.conf*.

```
search michaelwLucas.com bertjwregeer.com mwl.io
```

When you use a brief hostname, such as *www*, the resolver appends the first domain name in the search list. If there’s no answer, it repeats the query with the second domain name, and then the third. If I run *ping petulance*, the resolver searches for *petulance.michaelwLucas.com*, *petulance.bertjwregeer.com*, and *petulance.mwl.io*. If no such host exists in any of these domains, the search fails.

If you have neither *domain* nor *search* entries in */etc/resolv.conf*, but the machine’s hostname includes a domain name, the resolver uses the local machine’s domain name.

## The Nameserver List

Now that your resolver knows which domains to try, tell it which nameservers to query. List each in */etc/resolv.conf* on its own line, in order of preference. Use the keyword *nameserver* and the DNS server’s IP address. The resolver queries the listed nameservers in order. A complete *resolv.conf* might look like this:

```
domain mwl.io
nameserver 127.0.0.1
nameserver 203.0.113.8
nameserver 192.0.2.8
```

This resolver is ready to rock.

Note the first nameserver entry, though. The address 127.0.0.1 is always attached to the local host. This machine is running a local recursive nameserver. You can too!

## Caching Nameserver

Your host needs to perform a DNS lookup every single time it must contact a host. A busy server makes a whole bunch of queries, and by itself, the resolver doesn't cache any of these responses. A host needs to connect to Google 500 times in a minute? That's 500 DNS lookups. While setting up an authoritative DNS server requires a specific skill set, configuring a local recursive server requires only one line in /etc/rc.conf. This lets your FreeBSD host cache its DNS responses while reducing network congestion and improving performance.

Enable the local nameserver with the rc.conf variable local_unbound_enable.

```
# sysrc local_unbound_enable=YES
local_unbound_enable: NO -> YES
```

You can now start the local nameserver.

```
# service local_unbound start
```

When you start the service the first time, unbound configures itself. It extracts your system's nameservers from /etc/resolv.conf and configures itself to forward all queries to those nameservers. The setup process then edits /etc/resolv.conf to point all queries at the local nameserver, running on the IP address 127.0.0.1.

When your host makes a DNS query, the resolver queries unbound. The local nameserver checks its cache to see whether it has a valid and unexpired answer for the query. If it doesn't have a cached response, unbound queries your preferred nameservers.

I recommend enabling local_unbound on every server that isn't a DNS server.

### Network Activity

Now that you're on the network, how can you see what's going on? There are several ways to look at the network, and we'll consider each in turn. Unlike many commercial operating systems, FreeBSD commands such as netstat(8) and sockstat(1) give you more information about the network than can possibly be healthy.

#### Current Network Activity

The general-purpose network management program netstat(8) displays different information depending on the flags it’s given. One common question people have is, “How much traffic is my system pushing right now?” The netstat(8) -w (for wait) option displays how many packets and bytes your system is processing. The -w flag takes one argument, the number of seconds between updates. Adding the -d (for drop) flag tells netstat(8) to include information about packets that never made it to the system. Here, we ask netstat(8) to update its display every five seconds:

```
# netstat -w 5 -d
input                 (Total)             output
packets  errs  idrops  bytes               packets  errs      bytes  colls  drops
  134    0     0        44068                23     0         1518   0     0
   33    0       0      42610                23     0         1518   0     0
--snip--
```

Nothing appears to happen when you enter this command, but in a few seconds, the display prints a single line of information. The first three columns describe inbound traffic, while the next three describe outbound traffic. We see the number of packets received since the last update 1, the number of interface errors for inbound traffic since the last update 2, and the number of inbound dropped packets 3. The input information ends with the number of bytes received since the last update 4. The next three columns show the number of packets the machine transmitted since the last update 5, the number of errors in transmission since the last update 6, and how many bytes we sent 7. We then see the number of network collisions that have occurred since the last update 8, and the number of packets that have been dropped 9. For example, in this display, the system received 34 packets 1 since netstat -w 5 -d started running.

Five seconds later, netstat(8) prints a second line describing the activity since the first line was printed.

You can make the output as detailed as you want and run it as long as you like. If you’d like to get updates every second, just run netstat -w 1 -d. If once a minute is good enough for you, netstat -w 60 -d will do the trick. I find a five-second interval most suitable when I’d actively watching the network, but you’ll quickly learn what best fits your network and your problems.

Hit CTRL-C to stop the report once you’ve had enough.

## What’s Listening on Which Port?

Another popular question is, “Which ports are open and what programs are listening on them?” FreeBSD includes sockstat(1), a friendly tool to answer this question. It shows both active connections and ports available for client use.

The sockstat(1) program not only lists ports listening to the network, but also any other ports (or sockets) on the system. Use the -4 flag to see IPv4 sockets and -6 to view IPv6. Here’s trimmed sockstat(1) output from a very small server:

```
# sockstat -4
USER     COMMAND    PID    FD PROTO  LOCAL ADDRESS           FOREIGN ADDRESS

mwlucas  sshd       11872  4  tcp4   203.0.113.43:22       24.192.127.92:62937
root     sendmail   11433  4  tcp4   *:25                 *.*
www      httpd      9048   16 tcp4   *:80                 *.*
root     sshd       573    3  tcp4   *:23                 *.*
root     sshd       426    3  tcp4   *:22                 *.*
bind     named      275    20 udp4   203.0.113.8:53        *.*
bind     named      275    20 tcp4   203.0.113.8:53        *.*
```

The first column gives us the username that’s running the program attached to the port in question. The second column is the name of the command. We then have the process ID of the program and the file descriptor number attached to the socket. The next column shows what transport protocol the socket uses—either tcp4 for TCP on TCP/IP version 4, or udp4 for UDP on TCP/IP version 4. We then list the local IP address and port number, and finally the remote IP address and port number for each existing connection.

Take a look at our very first entry. I’m running the program sshd 1. A man page search takes you to sshd(8), the SSH daemon. The main sshd(8) daemon forked a child process on my behalf to handle my connection, so we see multiple instances of sshd(8) with different process IDs. I’m connected to the local IP address 203.0.113.43 2 on TCP port 22. The remote end of this connection is at the IP address 24.192.127.92 3 on port 62937. This is an SSH connection from a remote system to the local computer.

Other available connections include Sendmail 4, the mail server, running on port 25. Note that this entry doesn’t have any IP address listed as the foreign address. This socket is listening for incoming connections. Our httpd process 5 is listening for incoming connections on port 80.

The astute among you might notice that this server has two SSH daemons available for incoming connections, one on port 23 6 and one on port 22 7. As /etc/services shows, SSH normally runs on port 22 while port 23 is reserved for telnet. Anyone who telnets to this machine will be connected to an SSH daemon, which won’t work as they expect. The suspicious among you might suspect that this SSH server was set up to waltz around firewalls that only filter traffic based on source and destination ports and not the actual protocol. (I have no comment on such allegations.)

The last two entries are for a nameserver, named, awaiting incoming connections on port 53. This nameserver is listening for both UDP 8 and TCP 9 connections and is attached to the single IP address 203.0.113.8.

### Port Listeners in Detail

While sockstat(1) provides a nice high-level view of network service availability, you can get a little more detailed information about individual connections with netstat(8). To view open network connections, use netstat(8)’s -a flag. The -n flag tells netstat(8) not to bother translating IP addresses to hostnames; not only can this

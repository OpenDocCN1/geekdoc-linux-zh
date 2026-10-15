
```
192.0.2.0/24 ;     // Sample addresses, like example.com
224.0.0.0/3 ;       // Multicast address space
10.0.0.0/8 ;        // Private address space (RFC1918)²⁵
172.16.0.0/12 ;     // Private address space (RFC1918)
192.168.0.0/16 ;    // Private address space (RFC1918)
};
```

```
acl cunets {      // ACL for University of Colorado networks
    128.138.0.0/16 ;  // Main campus network
    198.11.16/24 ;
    204.228.69/24 ;
};
```

In the global options section of your config file, you could then include

```
allow-recursion { cunets; };
blackhole { bogusnets; };
```

It's also a good idea to restrict zone transfers to legitimate slave servers. An ACL makes things nice and tidy.

```
acl ourslaves {
    128.138.242.1 ;    // anchor
    ...
};
```

```
acl measurements {
    198.32.4.0/24 ;    // Bill Manning's measurements, v4 address
    2001:478:6:0::/48 ; // Bill Manning's measurements, v6 address
};
```

The actual restriction is implemented with a line such as

```
allow-transfer { ourslaves; measurements; };
```

Here, transfers are limited to our own slave servers and to the machines of an Internet measurement project that walks the reverse DNS tree to determine the size of the Internet and the percentage of misconfigured servers. Limiting transfers in this way makes it impossible for other sites to dump your entire database with a tool such as dig (see page 677).

Of course, you should still protect your network at a lower level through router access control lists and standard security hygiene on each host. If those measures are not possible, you can refuse DNS packets except to a gateway machine that you monitor closely.

## Open resolvers

An open resolver is a recursive, caching name server that accepts and answers queries from anyone on the Internet. Open resolvers are bad. Outsiders can consume your resources without your permission or knowledge, and if they are bad guys, they may be able to poison your resolver's cache.

Worse, open resolvers are sometimes used by bad guys to amplify distributed denial of service attacks. The attacker sends queries to your resolver with a faked source address that points back to the victim of the attack. Your resolver dutifully answers the queries and sends some nice fat packets to the victim. The victim didn’t initiate the queries, but it still has to route and process the network traffic. Multiply by a bunch of open resolvers and it’s real trouble for the victim.

Statistics show that between 75% and 80% of caching name servers are currently open resolvers—yikes! The site dns.measurement-factory.com/tools can help you test your site. Go there, select the “open resolver test,” and type in the IP addresses of your name servers. You can also test all the name servers on your network or all the servers at your site by using your whois identifier.

Use access control lists in named.conf or unbound.conf to limit your caching name servers to answering queries from your own users.

## Running in a chrooted jail

If hackers compromise your name server, they can potentially gain access to the system under the guise of the user as whom it runs. To limit the damage that someone could do in this situation, you can run the server in a chrooted environment, run it as an unprivileged user, or both.

For named, the command-line flag `-t` specifies the directory to chroot to, and the `-u` flag specifies the UID under which named should run. For example, `$ sudo named -u 53` initially starts named as root, but after named completes its rooty chores, it relinquishes its root privileges and runs as UID 53.

For nsd and unbound, the config file server options username and chroot do the same job. These options can also be specified on the nsd command line with the same flags as BIND: -u and -t, respectively.

Many sites don’t bother to use the -u and -t flags, but when a new vulnerability is announced, they must be faster to upgrade than the hackers are to attack.

The chroot jail cannot be an empty directory since it must contain all the files the name server normally needs in order to run: /dev/null, /dev/random, the zone files, configuration files, keys, syslog target files and the syslog UNIX-domain socket, /var, etc. It takes a bit of work to set this all up. The chroot system call is performed after libraries have been loaded, so it is not necessary to copy shared libraries into the jail.

## Secure server-to-server communication with TSIG and TKEY

While DNSSEC (covered in the next section) was being developed, the IETF developed a simpler mechanism, called TSIG (RFC2845), to allow secure communication among servers through the use of “transaction signatures.” Access control based on transaction signatures is more secure than access control based on IP

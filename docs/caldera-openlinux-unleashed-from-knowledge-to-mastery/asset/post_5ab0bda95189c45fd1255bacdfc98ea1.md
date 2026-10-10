
## TIS Configuration Updates

-FWTKSRCDIR=/u/b/mjr/firewall/fwtk
+FWTKSRCDIR=/usr/local/tis/src
# Location of X libraries for X-qw
-XLIBDIR=/usr/X11/lib
+XLIBDIR=/usr/X11R6/lib
# Location of X include files
-XINCLUDE=/usr/X11/include
+XINCLUDE=/usr/X11R6/include

Then in the file firewall.h change as follows:

#ifndef PERMFILE
-#define PERMFILE "/usr/local/etc/netperm-table"
+#define PERMFILE "/usr/local/tis/netperm-table"
#endif

Then save the changes to firewall.n and type the following:

# make
# make install

The most critical file in TIS is the proprietary netperm-table file, which is the “traffic cop” of connections through the TIS protocols over the firewall. Inside this file are such entries as user and group authentication from within the firewall and from without. For this reason, a TIS installation is conducted either by a chief administrator or in conjunction with network security authorities at the local site.

Assuming authentication has been correctly set up, additional features include custom tuning of timeouts to prevent multiple assaults on login sessions from Internet hacking tools such as Satan and Cracker.

While TIS excels at providing secure Telnet and FTP sessions, it should be understood that a proxy service of any sort still effectively shuts off the internal network from the external, so such common Internet features as chat, mail, and streaming multimedia will require much deeper consideration and greater configuration.

An example config for Telnet proxying follows:

in /usr/local/tis/netperm-table:
# Netacl Rules
netacl-telnetd: permit-hosts 127.0.0.1 -exec /usr/sbin/telnetd
# if the next line is uncommented, the telnet proxy is available
netacl-telnetd: permit-hosts * -exec /usr/local/tis/tn-gw
# Telnet Gateway Rules
tn-gw:               timeout 3600
tn-gw:               permit-hosts 192.168.7.*

Make sure nothing is running on the Telnet port (23) and start `netacl` as follows:

# /usr/local/tis/netacl -daemon telnet telnetd

Alternatively, the system's /etc/inetd.conf file, which controls the behavior of the "super server" daemon known as inetd (it acts as overseer of many typical Internet protocols on a local UNIX or Linux machine), may be edited to include specific instructions on how the new TIS protocol versions will be handled.

The following is an example of how the line would look in /etc/inetd.conf:

telnet stream tcp nowait root /usr/local/tis/netacl telnetd

Once this is done, users should be greeted by the following:

$ telnet comnet
Trying 192.168.7.1 ... 
Connected to comnet.thenetoffect.com.
Escape character is '^]' .
comnet.thenetoffect.com telnet proxy (Version V2.1) ready:
tn-gw->

At the `tn-gw->` prompt, the user can then connect to an outside host by typing `connect hostname` or `c hostname`.

The important point is that forwarding is shut off and no services, except of course the FWTK ones you need, are used. This will provide an extremely secure proxy setup.

With TIS, Telnet and FTP sessions are not transparently conducted for end users, but external access points using those protocols are. Thus, a user would open a Telnet session with the TIS Telnet daemon, which would open an acceptable portal through the firewall and allow the external session to piggyback over it. FTP is handled similarly.

## Putting Squid to Work

The proxy server known as Squid uses Internet caching to reduce the number of external connections from a local area network, while also speeding up the response to the local clients if the material is within the cache.

Many philosophical issues are at play when implementing any sort of Internet caching. The server is effectively making an external connection on behalf of the local client and conducting all of the transactions as if it was the inner client.

The implication is that the contents of the cache may now contain extremely private or sensitive material, such as credit card numbers, personal data, corporate secrets, and other highly important items. Additionally, legal precedent has yet to be set on whether the caching (copying) of material constitutes copyright infringement.

# PART II

As mentioned previously, a cache may not even be suitable if the majority of external connections go out to particularly dynamic Internet resources. The benefits of caching in such cases may be meager.

Once you have decided that Squid is for you (and you would certainly be following in the footsteps of many large installations and ISPs if you did so), you have to deal with building and installing it. (It doesn't come with the default OpenLinux). This is another package that uses autoconf, so it is relatively simple to get going (though there are some advanced options you need to be aware of).

Before installing Squid, you need to seriously consider how many clients will be using your cache and plan your hardware and installation requirements around that. For 5 to 10 workstations, 64 to 128MB of RAM and a gig of disk space should do well in improving your Web surfing experience. The hardware requirements can grow to tremendous proportions as you add users, however, and putting a lot of people behind a too-small cache is likely to slow down access to the Internet rather than speed it up.

A major part of a caching proxy server system is the configuration and management of large disk quantities, sometimes in the 10- to 20-gigabyte range of space for large local area networks. Without a solid understanding of disk hardware management, the task of setting up Squid could be difficult. The simplest implementation would be an assignment (in squid.conf) of all caching to one disk, but this results in the presence of a physical choke point as many users try to access that disk.

For large disk systems, even using RAID, Squid allows assignment of multiple caches across that disk real estate in a wide variety of configuration options.

By default, the software installs to `/usr/local/squid`. If you have a particular place with more space and faster disks, you can set that by invoking *configure* as

$ ./.configure --prefix=/path/to/squid*

Some other *configure* options you might want to set are as follows:

- **-enable-gnuregexp**: Compiles GNUregexp, a purportedly superior Regular Expression library for Squid to use.
- **-enable-icmp**: Enables ICMP pinging. This feature allows Squid to map other caches and destination sites to determine which cache is the closest from which to retrieve cached data, or whether it should retrieve the URL directly.
- **-enable-delay-pools**: Enables delay pools to limit bandwidth usage. This can be used as a type of “traffic shaper”; that is, it can effectively limit the bandwidth of client computers to a pre-determined amount.
- **-enable-useragent-log**: Enables logging of User Agent header. This turns on logging of User Agent headers, the HTTP header that identifies the type of Web browser being used.
- **-enable-snmp**: Enables SNMP monitoring. Allows you to monitor your cache using the Simple Network Monitoring Protocol.
- **-disable-ident-lookups**: This allows you to remove code that performs ident (RFC 931) lookups. This might be extremely useful at sites with predominantly Windows clients that don't generally run an ident.

Once you have decided on your options, then you need only to type

# make all
# make install

Squid will be built and placed where you have specified.

Squid actually has only one configuration file—which may seem simple but is not. Squid's squid.conf file can start out rather basic, but it soon takes on a life of its own on larger installations. For this reason, taking care to make clear comments inside it is highly recommended, and backing it up for safekeeping is critical. Before configuring the squid.conf file, a great deal of prior information should be accumulated. Since this file controls incoming and outgoing requests, timeout measures, firewall access information, HTTP port number assignment, and other important values, setting it up should not be done with guesswork. A clear picture of the network and firewall should be hashed out beforehand.

A sample squid.conf file will be installed into prefix/etc (where prefix is the location in which you installed). You MUST configure this file for your site before you start Squid. All of the options are commented out. You should uncomment and change the ones you need to, but no others.

Some of the important options you may have to set are as follows:

| **Option**             | **Description**                                                                 |
|------------------------|----------------------------------------------------------------------------------|
| `http_port`            | This defaults to 3128; another popular port is 8080. This is the port your browsers will have to point to. This line can contain multiple port numbers. |
| `tcp_incoming_address`  | These set the addresses Squid will bind to when it starts. By default, it will bind to all interfaces, but for security reasons you may want to change these to be specific addresses (for example, in a multi-homed situation). |
| `tcp_outgoing_address`  |                                                                                   |
| `udp_incoming_address`  |                                                                                   |
| `udp_outgoing_address`  |                                                                                   |

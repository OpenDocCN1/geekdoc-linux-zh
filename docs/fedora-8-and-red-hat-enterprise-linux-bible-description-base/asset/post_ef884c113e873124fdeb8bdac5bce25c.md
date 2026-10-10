
## TCP Wrappers and Access Control

of Red Hat Linux, the TCP wrapper daemon (`tcpd`) was used to facilitate this sort of selective access. In the current version of Fedora, TCP wrapper support has been integrated into `xinetd`. `xinetd` will look at the files `/etc/hosts.allow` and `/etc/hosts.deny` to determine when a particular connection should be granted or refused for services such as `login`, `rsh`, `telnet`, `finger`, and `talk`. TCP wrappers are also enabled by default for other services, such as a `vsftpd` FTP server (with `tcp_wrappers=YES` in your `vsftpd.conf` file).

When a service is requested that relies on TCP wrappers, the `hosts.allow` and `hosts.deny` files are scanned and checked for an entry that matches the IP address of the connecting machine. These checks are made when connection attempts occur:

- If the address is listed in the `hosts.allow` file, the connection is allowed and `hosts.deny` is not checked.
- If the address is in `hosts.deny` (but not the `hosts.allow` file), the connection is denied.
- If the address is in neither file, the connection is allowed.

It is not necessary (or even possible) to list every single address that may connect to your computer. The `hosts.allow` and `hosts.deny` files enable you to specify entire subnets and groups of addresses. You can even use the keyword `ALL` to specify all possible addresses. You can also restrict specific entries in these files so they apply only to specific network services. Look at an example of a typical pair of `hosts.allow` and `hosts.deny` files. Here's the `/etc/hosts.allow` file:

```
#
# hosts.allow   This file describes the names of the hosts which are
#               allowed to use the local INET services, as decided
#               by the '/usr/sbin/tcpd' server.
#
#
cups-lpd: 199.170.177.
  in.telnetd: 199.170.177... linumtoxys.net
  vsftpd: ALL
```

Here's the `/etc/hosts.deny` file:

```
#
# hosts.deny    This file describes the names of the hosts which are
#               *not* allowed to use the local INET services, as
#               decided by the '/usr/sbin/tcpd' server.
#
#
ALL: ALL
```

The preceding example is a rather restrictive configuration. It allows connections to the `cups-lpd` and `telnet` services from certain hosts, but then denies all other connections. It also allows connections to the FTP service (`vsftpd`) to all hosts. Let's examine the files in detail.

### Configuring TCP Wrappers

As usual, lines beginning with a # character are comments and are ignored by `xinetd` when it parses the file. Each noncomment line consists of a comma-separated list of daemons followed by a colon (: ) character and then a comma-separated list of client addresses to check. In this context, a client is any computer that attempts to access a network service on your system.

A client entry can be a numeric IP address (such as `199.170.177.25`) or a hostname (such as `jukebox.linuxtoys.net`), but is more often a wildcard variation that specifies an entire range of addresses. A client entry can take four different forms. The online manual page for the `hosts.allow` file describes them as follows:

- **A string that begins with a dot (.) character.** A hostname is matched if the last components of its name match the specified pattern. For example, the pattern `.tue.nl` matches the hostname `wzw.win.tue.nl`.
- **A string that ends with a dot (.) character.** A host address is matched if its first numeric fields match the given string. For example, the pattern `131.155.` matches the address of (almost) every host on the Eindhoven University network (`131.155.x.x`).
- **A string that begins with an at (@) sign is treated as an NIS netgroup name.** A hostname is matched if it is a host member of the specified netgroup. Netgroup matches are not supported for daemon process names or for client user names.
- **An expression of the form *n.n.n.n/m.m.m.m* is interpreted as a net/mask pair.** A host address is matched if *net* is equal to the *bitwise and* of the address and the mask. For example, the net/mask pattern `131.155.72.0/255.255.254.0` matches every address in the range `131.155.72.0` through `131.155.73.255`.

The example `hosts.allow` contains the first two types of client specification. The entry `199.170.177.` will match any IP address that begins with that string, such as `199.170.177.25`. The client entry `linuxtoys.net` will match hostnames such as `jukebox.linuxtoys.net` or `picframe.linuxtoys.net`.

Let’s examine what happens when a host named `jukebox.linuxtoys.net` (with IP address `199.170.179.18`) connects to your Fedora system using the Telnet protocol:

1. `xinetd` receives the connection request.
2. `xinetd` begins comparing the address and name of `jukebox.linuxtoys.net` to the rules listed in `/etc/hosts.allow`. It starts at the top of the file and works its way down the file until finding a match. Both the daemon (the program handling the network service on your Fedora box) and the connecting client’s IP address or name must match the information in the `hosts.allow` file. In this case, the second rule that is encountered matches the request:

   ```
   in.telnetd: 199.170.177.,    .linuxtoys.net
   ```

3. Jukebox is not in the `199.170.177` subnet, but it is in the `linuxtoys.net` domain. `xinetd` stops searching the file as soon as it finds this match.

How about if Jukebox connects to your box using the CUPS-lpd protocol? In this case, it matches none of the rules in `hosts.allow`; the only line that refers to the `lpd` daemon does not refer to the 199.170.179 subnet or to the `linuxtoys.net` domain. `xinetd` continues on to the `hosts.deny` file. The entry `ALL: ALL` matches anything, so `tcpd` denies the connection.

The ALL wildcard was also used in the `hosts.allow` file. In this case, we are telling `xinetd` to permit absolutely any host to connect to the FTP service on the Linux box. This is appropriate for running an anonymous FTP server that anyone on the Internet can access. If you are not running an anonymous FTP site, you probably should not use the `ALL` flag.

A good rule of thumb is to make your `hosts.allow` and `hosts.deny` files as restrictive as possible and then explicitly enable only those services that you really need. Also, grant access only to those systems that really need access. Using the `ALL` flag to grant universal access to a particular service may be easier than typing in a long list of subnets or domains, but better a few minutes spent on proper security measures than many hours recovering from a break-in.

> TIP: You can further restrict access to services using various options within the `/etc/xinetd.conf` file, even to the point of limiting access to certain services to specific times of the day. Read the manual page for `xinetd` (by typing `man xinetd` at a command prompt) to learn more about these options.

## Checking Log Files

Preparing your system for a cracker attack is only part of the battle. You must also recognize a cracker attack when it is occurring. Understanding the various log files in which Fedora and RHEL record important events is critical to this goal. The log files for your Fedora or RHEL system can be found in the `/var/log` directory.

Because the system logs are plain text files, you can view the contents of logs directly using any text editor or paging command (such as `less` or `more`). The logwatch facility (which comes with Fedora and RHEL) sends daily highlights from your log files in an e-mail message to the root user. You can also add packages, such as logwatch, to monitor your log files. (A description of logwatch is contained on the Wiley Web site for this book at `www.wiley.com/go/fedora8biblie`.)

### Understanding the syslogd service

Most of the files in the `/var/log` directory are maintained by the `syslogd` service. The `syslogd` daemon is the System Logging Daemon. It accepts log messages from a variety of other programs and writes them to the appropriate log files. This is better than having every program write directly to its own log file because it allows you to centrally manage how log files are handled. It is possible to configure `syslogd` to record varying levels of detail in the log files. It can be told to ignore all but the most critical message, or it can record every detail.

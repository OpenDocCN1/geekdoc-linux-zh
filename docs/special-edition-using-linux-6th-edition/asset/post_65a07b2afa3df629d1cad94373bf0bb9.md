
twist must be the last option on the line. Instead of invoking the ftp daemon, the previous line sends a 421 message to any client matching the in.ftpd rule.

Other options include: keepalive, linger, rfc931, banner, nice, setenv, umask, and user. These are used as follows:

- **keepalive** *(no arguments)*—The server periodically sends a keepalive packet to the client. If the client does not respond, the server terminates. This is useful for users who turn off their machines while still connected to the server.
- **linger** *<number of seconds>*—Length of time the kernel is to continue to try to send undelivered data to the client after a connection is closed.
- **rfc931** *[ timeout in seconds ]*—Perform RFC 931 username lookups. Only valid for TCP. If the client is not running IDENT or a similar RFC 931 service (as is the case with many PCs), noticeable connection delays can result. Timeout is optional; if it is not specified, compile-time default is used.
- **banner** *</some/path>*—Look in */some/path/* for a file with the same name as the daemon process (for example, in.telnetd for the telnet service), and then copy its contents to the client. This option uses character expansion within the file (explained as follows). Banners only work with TCP connections.
- **nice** *[ number ]*—Change the nice value from its default of 10.
- **setenv** *<name value>*—Used to set environment variables for those daemons that don’t reset their environment on startup. The *value* is subject to character expansion.
- **umask** *<octal>*—Similar to the shell umask variable.
- **user** *<user[.group]>*—Sets the daemon’s user and, optionally, the group.

## CHARACTER EXPANSION

The following character expansions can be used as noted previously:

- **%a (%A)**—The client (server) host address.
- **%c**—Returns client information depending on what’s available. Can be a user@host or IP address, or just an IP address.
- **%d**—The daemon process name (for example, in.telnetd).
- **%h (%H)**—Client (server) hostname or IP address.
- **%n (%N)**—Client (server) hostname (or unknown or paranoid if not available).
- **%p**—Daemon process ID.
- **%s**—Server information: daemon@host or IP address, or just a daemon name, depending on available information.
- **%u**—Username (or unknown).
- **%%**—Expands to single %.

## Miscellaneous Concerns

There are, however, some problems with implementing tcpd for all services. As noted earlier, r commands and NFS won't work effectively—if at all—and neither will RPC-based services (indicated by rpc/tcp) work. Another stopping point comes from the use of wait instead of nowait with services. A service using wait lingers on the queue for other connections. TCP wrappers log only the first connection request (the one that spawned the service), but not any subsequent ones while the same service is still alive. So a second connection can occur with no logging for daemons already sitting on the wait queue.

Do not use TCP wrappers with the Apache Web Server. Apache has the TCP wrappers functionality built into it. Use of tcpd in this case is redundant. The Apache configuration is similar to tcpd, so it will be understandable to anyone already familiar with tcpd.

## tcpdchk

tcpdchk is a utility that enables you to see what kind of syntax errors you've made while creating your /etc/hosts.allow file. The utility has several options, including -d; this option enables you to start from a directory other than /etc, create your hosts.allow file, and then test against that file before reporting the one that you are currently using. The -d option reads the hosts.allow file in the current directory (rather than in /etc). Obviously, this option is somewhat limiting if you are already in /etc.

By using the -v option, you can see every line that tcpdchk is reading and how it operates. See Listing 34.1 for a sample output.

### LISTING 34.1  SAMPLE tcpdchk TEST OUTPUT

```text
# tcpdchk -v
Using network configuration file: /etc/inetd.conf

>>> Rule /etc/hosts.allow line 1:
daemons:  ALL
clients:  .void.org EXCEPT dab@bar.void.org
option:   ALLOW
access:   granted

>>> Rule /etc/hosts.allow line 2:
daemons:  ALL EXCEPT in.telnetd
clients:  dab@bar.void.org
option:   ALLOW
access:   granted

>>> Rule /etc/hosts.allow line 4:
daemons:  in.telnetd
clients:  dab@bar.void.org
option:   spawn (/usr/sbin/safe_finger -l @client_hostname | /usr/bin/mail root) &
option:   DENY
access:   denied

>>> Rule /etc/hosts.allow line 5:
daemons:  in.ftpd
clients:  ALL
option:   ALLOW
access:   granted

>>> Rule /etc/hosts.allow line 6:
daemons:  ALL
clients:  ALL
option:   DENY
access:   denied
```

If tcpdchk is having trouble finding your /etc/inetd.conf file, -i path/to/inetd.conf can be used.

Finally, the -a option checks for any ALLOWs that aren’t explicitly declared—that is, which daemons can be started by a client as a result of omitting a statement to specifically ALLOW them.

## tcpdmatch

The tcpdmatch utility enables you to test specific examples against your configuration files. Again, tcpdmatch enables you to test against a hosts.allow file in your current directory by specifying the -d option. It also recognizes the -i path/to/inetd.conf if tcpdmatch has trouble finding it.

The syntax for tcpdmatch is as follows:

```text
tcpdmatch daemon[@server] [user@]client
```

The server option is for multihomed hosts, and the user is for specific users at a client. See Listing 34.2 for sample tcpdmatch output.

### LISTING 34.2  FOUR SAMPLE tcpdmatch OUTPUTS

```text
# tcpdmatch in.telnetd bar
warning: bar: hostname alias
warning: (official name: bar.void.org)
client:  hostname bar.void.org
client:  address 192.168.0.2
server:  process in.telnetd
matched: /etc/hosts.allow line 1
option:  ALLOW
access:  granted

# tcpdmatch in.telnetd dab@bar
warning: bar: hostname alias
warning: (official name: bar.void.org)
client:  hostname bar.void.org
client:  address 192.168.0.2
client:  username dab
server:  process in.telnetd
matched: /etc/hosts.allow line 4
option:  SPAWN (/usr/sbin/safe_finger -l bar.void.org | /usr/bin/mail root) &
option:  DENY
access:  denied

# tcpdmatch in.ftpd rim.caldera.com
client:  hostname rim.caldera.com
client:  address 207.179.39.2
server:  process in.ftpd
matched: /etc/hosts.allow line 5
option:  ALLOW
access:  granted

# tcpdmatch in.telnetd rim.caldera.com
client:  hostname rim.caldera.com
client:  address 207.179.39.2
server:  process in.telnetd
matched: /etc/hosts.allow line 6
option:  DENY
access:  denied
```

## CASE STUDY: SITE CONSTRUCTION

Putting together all you’ve learned, you can now construct a good `/etc/hosts.allow` for your site. Here, you’ll do just that.

First, see what is enabled. Use the following command to get your listing (it might be different from the text):

```sh
grep -v ^# /etc/inetd.conf | grep -v ^$ | grep -v internal
```

The preceding command line searches `/etc/inetd.conf` and excludes lines (`-v`) that begin with `#`. The results are piped to another `grep`, which excludes blank lines (shown as the regular expression `^$`), and then excludes lines with the word internal:

```text
ftp      stream  tcp     nowait  root    /usr/sbin/tcpd in.ftpd -l -a
telnet   stream  tcp     nowait  root    /usr/sbin/tcpd in.telnetd
pop3     stream  tcp     nowait  root    /usr/sbin/tcpd ipop3d
imap     stream  tcp     nowait  root    /usr/sbin/tcpd imapd
swat     stream  tcp     nowait.400 root /usr/sbin/tcpd swat
```

Now that you know what inetd is serving out to the world, you’re going to want to put some restrictions on who can access which servers. Your local network is `.void.org` with the `192.168.0/24` set of IP addresses. The following restrictions apply:

- **ftp**—Anyone can access ftp. It’s set up as an anonymous server. No special restrictions apply. PAM is denying access to any local users, such as root, that should not be using ftp.
- **telnet**—Only local systems can access telnet.
- **pop3**—Anyone can access from anywhere.
- **imap**—You have a local Web program to access imap but only via the local system. You don’t want to permit remote access except through the local Web server.
- **swat**—You want anyone on the local network to be able to administer Samba, but no remote access is to be allowed.

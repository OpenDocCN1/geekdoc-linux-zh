
script, and the service won’t run. You can still start it manually if you like, however, by typing the script’s name and, if needed, start or some other parameter to signal startup. You may need to disable the service again if you upgrade it, however, because the upgrade process may place a new initialization script in /etc/rc.d/init.d.

- Direct startup—You may need to remove an entry from /etc/rc.d/rc.local or some other startup file for some services. Most servers you install from RPMs don’t add lines to startup files in this way, but you may have done so for a few servers, particularly those that you compiled yourself. You can comment out such startup lines by preceding them with pound signs (#).

### Note

> Different distributions sometimes use different service startup protocols. Slackware, for instance, places most of its network startup commands in the /etc/rc.d/rc.inet1 and /etc/rc.d/rc.inet2 files. Consult your distribution’s documentation or a good book about your distribution for details.

Sifting through configuration files isn’t easy, and you may miss some services in this way. Therefore, you may want to use a port scanner, such as Nessus (http://www.nessus.org), to check what ports are open. There are also Internet-based services that will do this job, such as one available at http://www.dslreports.com. Port scanners may also be useful in checking the effectiveness of packet filtering firewalls or other measures.

## Using TCP Wrappers

One basic security measure employed by default in Red Hat Linux is known as TCP Wrappers. This is a tool that screens incoming connection requests. The TCP Wrappers daemon, tcpd, sits between inetd and the daemon for the requested service, as illustrated by Figure 24.3. When inetd receives a request for service, inetd passes that request, fairly indiscriminately, to the associated server—inetd isn’t primarily a security tool, but one to reduce the load on the system. TCP Wrappers, by contrast, serves as a filter, much as a personal secretary can filter phone calls. (My own personal fantasy is to have such a secretary who shields me from telemarketers, while quickly and unobtrusively passing calls from my friends, family, and editors at Sams. TCP Wrappers can do the equivalent for Linux daemons, but sadly not for voice telephone calls.)

![](img/5d4d3092919d1d16884788127447cc6d_598_0.png)

### Figure 24.3

TCP Wrappers may or may not be used for any given daemon, depending upon the configuration of the daemon and the inetd.conf configuration. (By default, Red Hat 6.0 actually sends finger requests through TCP Wrappers, but you could reconfigure it as shown here if you wanted to.)

The TCP Wrappers package is installed by default on Red Hat Linux 6.0, but the default configuration lets anybody connect to the system. You can tell tcpd to do filtering by creating appropriate entries in the /etc/hosts.allow or /etc/hosts.deny files. If you use the former, you block access to all hosts but those specified in the file, whereas if you use the latter file, you create a "black list" of sites to which you want to deny access. Both files' formats are the same, though; it's their meanings that are reversed. If a client appears in both hosts.allow and hosts.deny for a given service, hosts.allow takes precedence, and the client is given access.

The basic form of entries in both files is as follows:

```
daemon-list : client-list
```

These components are composed as follows:

- `daemon-list`—A list of daemons. These names appear in /etc/inetd.conf as the parameter to tcpd. You can also use wildcards for services, such as ALL (for any service).
- `client-list`—A list of client computers. Computer names can be specified as names (such as tyler or fillmore.threeroomco.com) or as IP addresses (such as 192.168.43.32). In both cases, you can specify an entire network by using a leading or trailing period, respectively (as in .threeroomco.com or 192.168.43.). TCP Wrappers also accepts a number of wildcards, such as ALL (any host) and LOCAL (hosts whose names don't contain dots). You can exclude one host from a rule by using the EXCEPT keyword, as in `192.168.43. EXCEPT 192.168.43.29`.

You should consult the hosts.allow or hosts.deny manpage (they're actually the same) for further details concerning the format of these files, including more advanced options to detect IP spoofing and the usernames of individuals requesting services.

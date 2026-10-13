To test the directive on one NTP server, you could change the **server** in each of the default directives to peer, as shown here:

```
peer 0.rhel.pool.ntp.org
peer 1.rhel.pool.ntp.org
peer 2.rhel.pool.ntp.org
```

Alternatively, you could be given the URI to an NTP peer server, perhaps on a corporate network, perhaps on a network that's been configured during the exam.

# Security Limits on NTP

As just described, the **restrict** directive from the /etc/ntp.conf configuration file can be used to limit access to a local NTP server. But that assumes an open port 123. Security limits can also refer to configured firewalls. Just be aware that an appropriate firewall rule for NTP opens up UDP (not TCP) port 123.

To test a connection to an NTP server, the `ntpq -p hostname` command can help. That command looks for the peers listed in the /etc/ntp.conf file. If the server is operational, you'll see something similar to the following output to the `ntpq -p localhost` command shown in Figure 17-8. Of course, if that command works from a remote system, using the local hostname or IP address, you've verified that the remote NTP server is operational.

![](bbox=[0.12, 0.45, 0.3, 0.49])

> ### Watch
> Since NTP is a UDP-based service, the telnet and nmap COMMANDS won't verify the operation of that service. You'll need a command like `ntpq -p hostname` for that purpose.

# FIGURE 17-8

```
[root@uai michael]# ntpq -p localhost
     remote          refid          st  t when poll reach  delay  offset  jitter
===============================================================================
 ntp.pox.org        192.5.41.40      2 u  30  64  17 103.586 462.252  10.857
ntp1.Housing.Be     169.229.128.214  3 u  22  64  17  38.452 462.901  12.111
ntp.sunflower.c     132.236.56.250   3 u  23  64  17  74.502 536.253   5.584
[root@uai michael]#
```

NTP server peers, verified with the `ntpq -p` command
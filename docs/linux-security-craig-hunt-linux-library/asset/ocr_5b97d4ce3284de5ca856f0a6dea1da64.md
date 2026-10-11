```
```
[ramon]$ tcpdmatch in.telnetd remote.example.com
client:      hostname remote.example.com
client:      address 207.55.44.67
server:      process in.telnetd
matched:     /etc/hosts.deny line 1
access:      denied
```
```

In the first two commands in Listing 4.9, you’re testing access to the ftp server, first using a local host as the destination and then using an external address as the destination. Given the tcpd configuration, the first request would be granted, while the second request would be denied. The third command example in Listing 4.9 probes access to the telnet daemon from a remote address, which is rightfully denied.

# TCP Wrappers Event Logging

One of the most useful features of TCP Wrappers, second to address-based filtering (filtering based on the IP address of the requesting client), is the ability to log every incoming network request, along with the result (grant/deny). As is the case with most Linux applications, TCP Wrappers uses the syslog facility to record events of interest. Examine your /etc/syslog.conf settings and look for the TCP Wrappers log events on the file where the authpriv.* facility gets directed (typically /var/log/secure):

```
```
[ramon]$ sudo tail -f secure
Oct 24 08:05:47 buggs in.telnetd[24257]: connect from elmer
Oct 24 08:06:07 buggs in.ftpd[24259]: connect from elmer
Oct 24 08:07:10 buggs in.rlogind[24261]: connect from elmer
Oct 24 21:04:42 buggs in.ftpd[25220]: connect from localhost
Oct 24 21:05:34 buggs in.telnetd[25228]: connect from goodguy
Oct 24 21:06:03 buggs in.fingerd[25232]: refused connect from badguy
```
```

Note that each entry in the output from this sudo command contains

+   - a timestamp
+   - the name of the host (buggs)
+   - the name of the network server
+   - the action, whether it was an accept (elmer, localhost, goodguy), or a denial (badguy)

It’s generally a good idea to configure swatch and/or logcheck to look for the keyword refused, and alert the staff of repeated unsuccessful connection requests, a sure sign of a brute-force attack.
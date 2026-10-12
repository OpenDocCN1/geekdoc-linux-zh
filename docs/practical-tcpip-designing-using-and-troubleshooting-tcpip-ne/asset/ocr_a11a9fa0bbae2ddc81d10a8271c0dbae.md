# 2. The /etc/services file

This file lists the port numbers corresponding to named network services. Just as the DNS makes it easy to use names instead of IP numbers for hosts, /etc/services lets you use names instead of numbers for ports. Figure A20.3 shows an annotated excerpt from the file on one of our Linux systems. Names are case sensitive, and fields are separated by tabs or spaces. Text after a “#” is treated as comment.

![](bbox=[0.1, 0.22, 0.88, 0.58])

Applications that use ports read this file to translate between port names and numbers. This is how, for example, you can say telnet http instead of telnet 80, and how tcpdump prints port names in its output:

```
alice.2796 > bob.uic.co.uk.www: . ack 1 win 8760 (DF)
```

Notice that some of the names are not what you expect, e.g. DNS is called domain or nameserver, not dns. You can edit the file and insert your own aliases for these names (but even if you do add extra aliases, we recommend that you keep the original name in the file too, as other programs may rely on it).

Many services have entries for both UDP and TCP transports, for the same port number. As we mentioned in Module 15.3, UDP and TCP ports are completely separate. When the protocols were being developed, the well-known UDP and TCP port numbers for a given service could have been made different, but for convenience the same ones were always chosen for both. You only need the entry in /etc/services if you are going to use the service in question; otherwise you can delete it (or more usually, comment it out). Many of the UDP entries are
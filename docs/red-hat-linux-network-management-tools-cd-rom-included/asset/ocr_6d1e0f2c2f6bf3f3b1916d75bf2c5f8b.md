```
```
650  open    udp     bwnfs
652  open    tcp     unknown
661  open    udp     unknown
671  open    udp     unknown
673  open    tcp     unknown
676  open    udp     unknown
678  open    tcp     unknown
681  open    udp     unknown
683  open    tcp     unknown
713  open    tcp     unknown
714  open    udp     unknown
800  open    udp     mbsm_daemon
1022 open    udp     unknown
1023 open    udp     unknown
1024 open    udp     unknown
1024 open    tcp     unknown
1026 open    udp     unknown
2049 open    udp     nfs
6000 open    tcp     X11

Nmap run completed -- 1 IP address (1 host up) scanned in 5
seconds
```
```

Note that now both UDP and TCP ports are displayed, sorted by port number.

As with any good port scanner, the ability to scan a particular port is paramount. One good way to determine if all the systems on a network have a standard set of network services or a particular service is to scan the network with a specific port number in mind. For example, assume we would like to determine if all the systems on the 10.0.2.0 network support some sort of SNMP agent. The command:

```
`$ nmap -p 161 -sU -o results 10.0.2.0/24`
```

tells **nmap** to scan port 161 (the SNMP port) on network 10.0.2.0 using UDP and then save the output information in a file called *results*. If we display this file, we find the following:

```
```
# Log of: nmap -p 161 -sU -o result 10.0.2.0/24
No ports open for host duree.home.com (10.0.2.10)
No ports open for host king.home.com (10.0.2.21)
No ports open for host derry.home.com (10.0.2.25)
Interesting ports on probe.home.com (10.0.2.50):
```
```

*(_continued)*
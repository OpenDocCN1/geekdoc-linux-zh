192.88.209.0-255 or ¹²⁸.88.209.*¹ all scan CERT’s Class C. SEE THE MAN PAGE FOR MORE THOROUGH EXPLANATIONS AND EXAMPLES

One of the strengths of **nmap** is that it supports many different scanning methodologies. Some scanners only support TCP scanning, which is very useful but has limitations. For instance, some networking devices don’t provide generic TCP networking services like traditional UNIX systems do; they may only support a limited set of UDP services. In this instance, using a port scanner that only supports TCP would be useless. Consider the following scan and associated output:

```
# nmap -sT probe.home.com

Starting nmap V. 2.12 by Fyodor (fyodor@hdp.com, www.insecure.org/nmap/)

Interesting ports on probe.home.com (10.0.2.50): (Not showing ports in state: filtered)

Port State Protocol Service

Nmap run completed -- 1 IP address (1 host up) scanned in 66 seconds
```

As you can see in this output, **nmap** didn’t detect any services on the target system. However, scanning using the -sU option instructs **nmap** to scan a range of UDP ports instead of the default TCP port range. Thus, interestingly enough,

```
# nmap -sU 10.0.2.50
```

yields the following output when executed:

```
WARNING: -sU is now UDP scan -- for TCP FIN scan use -sF

Starting nmap V. 2.12 by Fyodor (fyodor@hdp.com, www.insecure.org/nmap/)

Interesting ports on probe.home.com (10.0.2.50): (Not showing ports in state: filtered)

Port State Protocol Service
161 open udp snmp

Nmap run completed -- 1 IP address (1 host up) scanned in 12 seconds
```

We find an SNMP process listening on the standard 161 port. This tells us that this device only supports SNMP and nothing else. If we wanted, we could query the device further using SNMP.
```
TCP Sequence Prediction: Class=64K rule
Difficuity=1 (Trivial joke)
Remote operating system guess: HP-UX 10.20 E 9000/777 or A
7/12/60 with tcp_random_seq = 0

Nmap run completed -- 1 IP address (1 host up) scanned in 2 seconds
```

# # Windows NT System

# ## Description

This report was generated from an NT workstation. The services identified don't match any common UNIX services.

# ## Report Results

```
Starting nmap V. 2.12 by Fyodor (fyodor@dhp.com, www.insecure.org/nmap/)
Interesting ports on (10.0.2.124):
Port     State    Protocol   Service
135      open     tcp        loc-srv
139      open     tcp        netbios-ssn
427      open     tcp        srvloc

TCP Sequence Prediction: Class=trivial time dependency
Difficuity=13 (Easy)
Remote operating system guess: Windows NT4 / Win95 / Win98

Nmap run completed -- 1 IP address (1 host up) scanned in 1 second
```

# # Cisco Router System

# ## Description

This report show which services are available from a Cisco router.

# ## Report Results

```
[root@dymus /root]# nmap -0 199.82.24.1

Starting nmap V. 2.12 by Fyodor (fyodor@dhp.com,
www.insecure.org/nmap/)
Interesting ports on (10.0.2.1):
Port     State    Protocol   Service
7        open     tcp        echo
9        open     tcp        discard
13       open     tcp        daytime
19       open     tcp        chargen
```
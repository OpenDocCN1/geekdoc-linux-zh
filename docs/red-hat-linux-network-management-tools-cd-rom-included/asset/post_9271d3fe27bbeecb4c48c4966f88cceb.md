
containing the string: Host switch.home.com (10.0.2.60) appears to be up ... good. Note that the most important point with respect to this example is that nmap is very smart about probing non-existent or down systems; it didn't spend much time or resources probing unresponsive systems. Before nmap attempts to scan a device, it first determines if it is reachable on the network by performing a ping on it. This not only reduces the amount of time required to perform the scan and lessens system resources needed, but it helps to preserve network bandwidth as well. It is important not to underestimate the impact that scanning can have on a network, and nmap does a good job to reduce the network requirements while probing.

## Nmap Output Listing

The listing below shows some of the nmap output when it is used against a series of different computer systems and networking devices. Certainly your mileage may vary, but this tool is quite good at detecting different kinds of systems. This section includes both output and a general description of the systems and supported networking services. Since most of the systems support many of the same networking services and processes, the common ones are listed in Table 5.9.

### Table 5.9 Standard nmap network listings

| Port | Service Name | Description |
|------|--------------|-------------|
| 7 | echo | Echoes characters sent to this port; service provided by the inetd process; primarily used for testing |
| 8 | discard | Discards any data sent to it; acts like /dev/null for networking services and other networking applications; primarily used for testing |
| 13 | daytime | Provides time in human-readable format; primarily used for testing |
| 19 | chargen | Character generator; produces ASCII character set; primarily used for testing |
| 21 | ftp | Standard File Transfer Protocol Server |
| 23 | telnet | Telnet server; provides remote login services |
| 25 | smtp | Simple Mail Transfer Protocol; usually sendmail server is listening on this port |
| 37 | time | Provides machine-readable time |
| 53 | domain | Domain name server process |
| 79 | finger | Finger server process |
| 80 | http | Web server process |
| 111 | sunrpc | Sun Remote Procedure Calls services |
| 199 | snmp | SNMP master agent |
| 382 | hp-managed-node | HP agent. This process provides network management services for HP network manager products. |
| 512 | exec | Remote execution server with authentication |
| 513 | login | Remote login with authentication |
| 514 | shell | Remote shell server with authentication |
| 515 | printer | Remote printer server |
| 540 | uucp | UUCP server |
| 4045 | lockd | Lock daemon |

## AIX System

### Description

This report was generated from an RISC 6000 system running AIX 4.2. It includes some of the standard UNIX networking services and some specific ones as well.

### Report Results

Starting nmap V. 2.12 by Fyodor (fyodor@lhp.com, www.insecure.org/nmap/)

Interesting ports on lexis.home.com (10.0.2.240):

| Port | State | Protocol | Service |
|------|-------|----------|---------|
| 7 | open | tcp | echo |
| 9 | open | tcp | discard |
| 13 | open | tcp | daytime |
| 19 | open | tcp | chargen |
| 21 | open | tcp | ftp |
| 23 | open | tcp | telnet |
| 25 | open | tcp | smtp |
| 37 | open | tcp | time |
| 111 | open | tcp | sunrpc |
| 199 | open | tcp | smux |
| 382 | open | tcp | hp-managed-node |
| 512 | open | tcp | exec |
| 513 | open | tcp | login |
| 514 | open | tcp | shell |
| 515 | open | tcp | printer |
| 543 | open | tcp | klogin |
| 544 | open | tcp | kshell |
| 651 | open | tcp | unknown |
| 652 | open | tcp | unknown |
| 777 | open | tcp | unknown |
| 2401 | open | tcp | cvsserver |

TCP Sequence Prediction: Class=true random  
Difficulty=9999999 (Good luck!)

Remote operating system guess: AIX 4.2

*Nmap* run completed -- 1 IP address (1 host up) scanned in 4 seconds

## Solaris System

### Description

This report identifies the system called *chips* as either a Solaris 2.6 or a Solaris 2.7 system. In this case, the system is actually 2.6, but since there are relatively few differences between 2.6 and 2.7, *nmap* indicates both. Two interesting and unique services detected by *nmap* include *lotusnote* and *xaudio*. The first process represents a Lotus Notes Domino server, and the other is an audio/video application that provides multicast support.

### Report Results

Starting nmap V. 2.12 by Fyodor (fyodor@dhcp.com, www.insecure.org/nmap/)

Interesting ports on chips.home.com (10.0.2.199):

| Port | State | Protocol | Service |
|------|-------|----------|---------|
| 7 | open | tcp | echo |
| 9 | open | tcp | discard |
| 13 | open | tcp | daytime |
| 19 | open | tcp | chargen |
| 21 | open | tcp | ftp |
| 23 | open | tcp | telnet |
| 25 | open | tcp | smtp |
| 37 | open | tcp | time |
| 79 | open | tcp | finger |
| 80 | open | tcp | http |
| 111 | open | tcp | sunrpc |
| 512 | open | tcp | exec |
| 513 | open | tcp | login |
| 514 | open | tcp | shell |
| 515 | open | tcp | printer |
| 540 | open | tcp | uucp |
| 1103 | open | tcp | xaudio |
| 1352 | open | tcp | lotusnote |
| 4045 | open | tcp | lockd |
| 6112 | open | tcp | dtspc |
| 7100 | open | tcp | font-service |

TCP Sequence Prediction: Class=random positive increments  
Difficulty=48025 (Worthy challenge)

Remote operating system guess: Solaris 2.6 - 2.7

Nmap run completed -- 1 IP address (1 host up) scanned in 2 seconds

## HP-UX System

### Description

This system, called dip, provides many of the standard services and includes Klogin/Kshell for security login and remote shell execution on ports 543 and 544, respectively.

### Report Results

Starting nmap V. 2.12 by Fyodor (fyodor@nnp.com, www.insecure.org/nmap/)

Interesting ports on dip.home.com (10.0.2.198):

| Port | State | Protocol | Service |
|------|-------|----------|---------|
| 7 | open | tcp | echo |
| 9 | open | tcp | discard |
| 13 | open | tcp | daytime |
| 19 | open | tcp | chargen |
| 21 | open | tcp | ftp |
| 23 | open | tcp | telnet |
| 25 | open | tcp | smtp |
| 37 | open | tcp | time |
| 53 | open | tcp | domain |
| 94 | open | tcp | objcall |
| 111 | open | tcp | sunrpc |
| 113 | open | tcp | auth |
| 135 | open | tcp | loc-srv |
| 382 | open | tcp | hp-managed-node |
| 512 | open | tcp | exec |
| 513 | open | tcp | login |
| 514 | open | tcp | shell |
| 515 | open | tcp | printer |
| 543 | open | tcp | klogin |
| 544 | open | tcp | kshell |
| 590 | open | tcp | tns-cm1 |
| 659 | open | tcp | unknown |
| 661 | open | tcp | unknown |
| 816 | open | tcp | unknown |
| 980 | open | tcp | unknown |
| 984 | open | tcp | unknown |
| 988 | open | tcp | unknown |
| 993 | open | tcp | imaps |
| 996 | open | tcp | xtremeric |
| 1501 | open | tcp | sas-3 |
| 5520 | open | tcp | sdlog |
| 6111 | open | tcp | spc |
| 6112 | open | tcp | dtspc |

TCP Sequence Prediction: Class=64K rule  
Difficulty=1 (Trivial joke)

Remote operating system guess: HP-UX 10.20 E 9000/777 or A 7/12/60 with tcp_random_seq = 0

Nmap run completed -- 1 IP address (1 host up) scanned in 2 seconds

## Windows NT System

### Description

This report was generated from an NT workstation. The services identified don't match any common UNIX services.

### Report Results

Starting nmap V. 2.12 by Fyodor (fyodor@dhp.com, www.insecure.org/nmap/)

Interesting ports on (10.0.2.124):

| Port | State | Protocol | Service |
|------|-------|----------|---------|
| 135 | open | tcp | loc-srv |
| 139 | open | tcp | netbios-ssn |
| 427 | open | tcp | srvloc |

TCP Sequence Prediction: Class=trivial time dependency  
Difficulty=13 (Easy)

Remote operating system guess: Windows NT4 / Win95 / Win98

Nmap run completed -- 1 IP address (1 host up) scanned in 1 second

## Cisco Router System

### Description

This report shows which services are available from a Cisco router.

### Report Results

[root@dymus /root]# nmap -0 199.82.24.1

Starting nmap V. 2.12 by Fyodor (fyodor@dhp.com, www.insecure.org/nmap/)

Interesting ports on (10.0.2.1):

| Port | State | Protocol | Service |
|------|-------|----------|---------|
| 7 | open | tcp | echo |
| 9 | open | tcp | discard |
| 13 | open | tcp | daytime |
| 19 | open | tcp | chargen |

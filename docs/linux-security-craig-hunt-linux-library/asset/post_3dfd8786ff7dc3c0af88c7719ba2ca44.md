
It is surprisingly easy to sniff a network segment and fish for confidential information. In fact, the Linux revolution has exacerbated this problem, since even the most naïve user can use Linux’s ability to promiscuously inspect every packet that it sees on the wire. Not only can intruders capture the payload of network packets flying by, but they can also capture password information that they can use to stage a root compromise of the unsuspecting server.

> **WARNING** You should never, under any circumstance, allow the root password of your Linux server to traverse the network unencrypted.

To protect your root password, you should:

-   Disable root logins over the network.
-   Disable `telnet`, `rsh`, `rlogin`, and `ftp`.
-   Only use Secure Shell (`ssh`) for interactive logins.
-   Only use Secure Copy (`scp`) to transfer files to and from the server.

In addition, you should make use of Linux’s support for VPN technology, which uses strong cryptography to protect the entire conversation between your Linux server and any other host with which you need to exchange confidential information. Chapter 12 is devoted to the topic of VPNs in the Linux environment.

## Trojan Horses

You’ve all downloaded seemingly useful free software from the Internet, only to find out that its features were largely exaggerated. However, an increasing number of Linux servers are being infected by software that performs a very different task from the one it advertises. These so-called *Trojan horses* are programs that, though disguised as harmless applications, open up a back door through which intruders can exploit the system, often with root privileges. Just like the wooden artifact used by the Greeks to break into Troy during the war, the Trojan horse presents itself as a useful tool and is often partially functional. But even as it appears to serve its advertised purpose, it can cripple or destroy your server and often your entire network.

Trojan horses can be extremely difficult to detect. In fact, they are often disguised as security applications, so you can be shooting yourself in the foot while thinking you’re improving the overall security of the server. A good example of this surfaced in January 1999, when it was discovered that a widely distributed version of TCPWrappers was actually a Trojan horse. (See Chapter 4, “Network Services Configuration,” for a detailed description of TCPWrappers.) While originally designed to monitor and filter transport layer connections, the Trojan horse version of TCPWrappers had been modified to provide root access to would-be intruders.

Another feature common to most Trojan horse programs is their ability to inform attackers of the intrusion, providing them enough detail about your system so that they can stage a successful attack. The Trojan TCPWrappers was designed to send an e-mail to the intruder’s address that includes information about the infected system and about the unsuspecting user who installed the program.

You can protect yourself against Trojan horses by following these simple recommendations:

-   Download all your software from well-known Internet sites, or well-published mirrors of these primary sites.
-   Before you install the software, look for digital signatures or checksums to assure the integrity of downloaded package.
-   Make as much standard software as possible available to your users (as long as your security policy allows it). Keep it up to date.
-   Periodically monitor Trojan horse advisories from the CERT Coordination Center (www.cert.org).

In addition, you should conduct periodic scans of your server and look for suspicious network ports that are active or in LISTEN state. Listing 1.1 shows an execution of the netstat command that shows a server with a suspicious port (555) in LISTEN state. Note that the command has not been able to resolve port number 555 to a well-known number in the /etc/services file. This is an indication that the daemon is not a standard one and should be investigated further.

### Listing 1.1 Execution of the netstat command showing a suspicious daemon running on TCP port 555

```text
[ramon]$ netstat -a
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address     State
tcp        0      0 *:555               *:*                 LISTEN
tcp        0      0 *:ssh               *:*                 LISTEN
tcp        0      0 *:ftp               *:*                 LISTEN
udp        0      0 *:snmp              *:*                  
raw        0      0 *:icmp              *:*                    7
raw        0      0 *:tcp               *:*                    7
Active UNIX domain sockets (servers and established)
Proto RefCnt Flags    Type       State I-Node Path
unix 0 [ ACC ] STREAM LISTENING 491 /dev/log
unix 1 [ ] STREAM CONNECTED 985 @0000003d
unix 1 [ ] STREAM CONNECTED 886 @00000039
unix 1 [ ] STREAM CONNECTED 959 @0000003c
unix 1 [ ] STREAM CONNECTED 554 @00000021
unix 1 [ ] STREAM CONNECTED 740 @00000035
unix 0 [ ] STREAM CONNECTED 117 @00000013
unix 1 [ ] STREAM CONNECTED 744 @00000036
unix 1 [ ] STREAM CONNECTED 986 /dev/log
unix 1 [ ] STREAM CONNECTED 960 /dev/log
unix 1 [ ] STREAM CONNECTED 887 /dev/log
unix 1 [ ] STREAM CONNECTED 745 /dev/log
unix 1 [ ] STREAM CONNECTED 741 /dev/log
unix 1 [ ] STREAM CONNECTED 588 /dev/log
```

Chapter 5 contains a more detailed look into the tools available for monitoring your Linux server for this type of intrusion.

## Cryptanalysis and Brute Force Attacks

Most of the cryptographic algorithms in use today have proven to be robust enough to provide an appropriate level of confidentiality, integrity, and authentication. However, there have been several cases where some of these algorithms have been found to be vulnerable to attacks or mathematical exploits where the keyspace (the average number of combinations before the algorithm can be cracked) has been proven to be much smaller than initially thought. (By "mathematical exploits" I mean exploits that take advantage of flaws present in the functions used by the algorithm designers to derive prime numbers, generate keys, add entropy, and so on.)

In 1998 we saw a highly publicized case of cryptanalysis, where renowned security experts Bruce Schneier and "Mudge" discovered a number of security flaws in Microsoft's authentication algorithm for PPTP, a VPN protocol used in the Windows operating system. The MS-CHAP v.1 authentication algorithm was found to be vulnerable to password eavesdropping. In addition, the Microsoft Point-to-Point Encryption Algorithm (MPE) was also found to be much less effective than the 128-bit key strength that the vendor advertised, thereby exposing the user to eavesdropping attacks on the transmitted data. In 1999, Microsoft released MS-CHAP v.2 as an enhancement of the original version. However, a fundamental flaw still remains; the confidentiality of the VPN transmission is only as strong as the password that users choose for authentication.

There is a Linux version of PPTP (PoPTop, discussed in Chapter 12) that is fully interoperable with the Microsoft implementation and is, therefore, subject to the same password-guessing weakness.

This leads us to our last type of attack: brute force guessing of passwords and keys. As the computing power available to the average user increases at exponential rates, so does the potential for an intruder to guess your password or key. By employing a *brute force* approach, would-be attackers use idle computing power available to them in order to attempt to guess encryption keys until the correct one is found. These are also called *dictionary attacks*, because the attacker often uses a well-known dictionary to try to guess a password, based on the fact that most users tend to choose real words as their passwords.

The power of brute force attacks on cryptographic algorithms was best illustrated in the summer of 1998 when the Electronic Frontier Foundation (EFF) was able to crack the 56-bit key of the DES algorithm using a purpose-built computer at a cost of $250,000. The feasibility of these types of attacks has raised the bar for cryptographic strength, and has raised the awareness of the limitations of even the strongest cryptography in use today.

Now that you’ve seen who the enemies are and have taken a peek at their weapons of choice, let’s take a look at how you can orchestrate an appropriate defense, using some of the layers in the Open Systems Interconnect (OSI) model as a point of reference.

## The Layered Approach to Information Security

A lot of work has been devoted to the topic of adding security to the Linux kernel. There is now native kernel support for packet filtering, packet logging, masquerading, and even defense against denial of service attacks. This goes a long way toward securing the system itself, but are you willing to let intruders get all the way into the portals of your servers? An effective security policy is one that starts at the core of the Linux server, but keeps moving outward by including protection mechanisms outside of the system itself. Your defense should cover the network configuration of the server, the network applications that run on the server, the perimeter of the corporate network, and even the remote access clients used by road warriors to access corporate resources from the public Internet.

Let’s take a closer look at the considerations that apply to each of these layers. Note that this discussion will work its way outward from the Linux kernel toward the Internet.

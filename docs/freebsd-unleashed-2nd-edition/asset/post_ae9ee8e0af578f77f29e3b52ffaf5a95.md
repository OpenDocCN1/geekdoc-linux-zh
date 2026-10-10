
## Using tcpdump to Monitor Traffic

You can illustrate the risks inherent in your network's clear-text services by using a *packet sniffer*, a software tool that watches all packets on your network segment and displays the ones that interest you. A sniffer operates by putting your Ethernet card into "promiscuous mode," where it accepts all packets that it sees on the network, rather than discarding packets not addressed to it (for information on packets, see Chapter 21, "Networking with FreeBSD"). The sniffer then applies all kinds of highly configurable filters to the traffic it sees. This is how an eavesdropper can extract the relevant packets from the storm of traffic to capture a transaction with ominous ease.

FreeBSD's built-in packet sniffer is *tcpdump*, available in /usr/sbin. Its use is barred to regular users, who get a *Permission denied* error on the /dev/bpf0 (Berkeley Packet Filter) device; only the administrator (root) can use the program. The purpose of *tcpdump* is not to log the actual data of the TCP/IP packets it sees (you might want to look into *tcpflow*, available in the ports at /usr/ports/net/tcpflow or into WildPackets' EtherPeek for that functionality). Instead, *tcpdump* is much like Crack in that it's intended as an administrative security-auditing tool that allows you to see how much unencrypted traffic is being sent to and from your system, and to watch for suspicious network activity that might indicate illicit pursuits on the part of your users.

> **NOTE**
> It's possible to use *tcpdump* to spy on the activities of your users, regardless of whether they're doing anything wrong. A warning in the GENERIC kernel configuration file reminds you to consider the ethical issues involved with using a packet sniffer. It all depends on what kind of system you're running, naturally, but packet sniffers are the equivalent of telephone wiretaps or hidden security cameras, and you should use *tcpdump* only under circumstances in which you would be comfortable using wiretaps and hidden cameras to gather information.

The configuration of *tcpdump* is quite complex, and it allows you to do a lot of very useful and versatile things. All we're interested in right now, though, is demonstrating the dangers of clear-text TCP/IP traffic. Let's set up a simple monitoring filter on the Telnet port (TCP port 23):

```bash
# tcpdump -x port 23
tcpdump: listening on fxp0
20:14:19.076941 w044.z064402043.sjc.ca.dsl.c.nc.net.54109 >
w012.z064402043.sjc.ca.dsl.c.nc.net.telnet: S 1972342903:1972342903(0)
win 32768 <mss 1460,nop,nop,wscale 0,nop,nop,timestamp 465710> (DF) [tos 0x10]

4510 003c e44b 4000 4006 8024 0002 2b2c
4002 2b0c c35d 0017 758f 9077 0000 0000
a002 8000 001b 0000 0204 05b4 0103 0300
0101 800a 0007 1b2e 0000 0000

20:14:19.077050 w012.z064002043.sjc-ca.dsl.cnc.net.telnet >
. z064002043.sjc-ca.dsl.cnc.net.54109: S 1734674412:1734674412(0)
ack 1972342904 win 17520 <mss 1460> [DF]
4500 002c c9c2 4000 4006 9acd 4002 2b0c
4002 2b2c 0017 d35d 6765 07ec 758f 9078
6012 4470 349c 0000 0204 05b4

20:14:19.677472 w044.z064002043.sjc-ca.dsl.cnc.net.54109 >
w012.z064002043.sjc-ca.dsl.cnc.net.telnet: . ack 195 win 33580 [DF]
[tos 0x10]
4510 0028 e458 4000 4006 802b 4002 2b2c
4002 2b0c d35d 0017 758f 910a 6765 08af
5010 832c 0c49 0000 5555 5555 5555
^C
134 packets received by filter
0 packets dropped by kernel
```

The `-x` option tells tcpdump to output the first part of each packet's payload in hexadecimal; if this option is omitted, tcpdump only outputs the link-level headers. You may want to use `-w <filename>` to send tcpdump output into a file so that you can peruse it more easily.

Because tcpdump is not designed as “spyware,” it does not decode the hexadecimal output for you. You can, if you wish, convert it to plain human-readable text with a hex editor such as /usr/ports/editors/hexedit. However, if you're interested in the contents of the packets, you will want to use a different program (such as tcpflow).

## Adding Extra Security with Encrypted Protocols

The tcpdump data isn't encrypted at all. It only takes a little bit of effort to be able to see the complete contents of every packet sent via Telnet. It's even easier with tools that do the packet decoding for you, such as tcpflow, tcps show, and EtherPeek. If these packets contain a user's login session, an attacker using any of these programs would know the user's login password and could use it to log in to your system. This security gap endangers POP3, IMAP, FTP, and HTTP traffic, too, as well as just about every small and nonessential service, such as finger and Syslog. Safeguarding against the use of these sniffer programs is especially important in systems where passwords or any other sensitive data is transferred. Protecting communications is as much a privacy issue as it is a security concern.

Fortunately, there's a way to combat the problems of sniffer programs. You can use an encrypted alternative to any of the major data-transfer protocols, many of which are part of the default FreeBSD installation. For instance, SSH is a secure alternative to Telnet, and SSL is a method for encrypting Web traffic and other services. Sealing the security holes inherent in clear-text services is only a matter of knowing the encrypted versions exist, implementing them, and convincing your users to adopt them.

## Securing Terminal Traffic (SSH)

Terminal traffic, which is typically from the Telnet or `rlogin` application, is a result of remote users interacting with Unix systems; you are probably accustomed to connecting to your FreeBSD machine remotely both to use it and to perform your administration duties. However, terminal use is probably the riskiest type of clear-text traffic—and it's the easiest to fix. FreeBSD comes with a complete SSH (Secure Shell) package designed to supplant Telnet and `rlogin`. The SSH package is called OpenSSH, and it was developed originally for OpenBSD. OpenSSH allows users to establish a completely encrypted tunnel to your server, protecting their login passwords and any command-line activity from snooping intruders.

The SSH server, `sshd`, runs on port 22 as a standalone daemon that, like Apache, spawns off new `sshd` processes when new connections come in. To enable the SSH server, add the following line to `/etc/rc.conf` (if it's not already there) and then reboot (or simply type `sshd`):

```bash
sshd_enable="YES"
```

The SSH client is a replacement for Telnet. To use it instead of the command-line `telnet` program, issue the `ssh` command instead of the `telnet` command:

```bash
# ssh strip es.somewhere.com
```

Instead of letting the server issue its own `Login:` and `Password:` prompts, the SSH client itself prompts for your password, assuming the remote username is the same as the local one. You can specify an alternate username with either of a couple of different methods:

```bash
# ssh strip es.somewhere.com -l frank
# ssh frank@stripes.somewhere.com
```

The `ssh` program establishes the encrypted connection and passes the login data to the server in a secure fashion. From that point on, it acts just like a regular Telnet connection—there's no difference as far as the user is concerned. A user on a FreeBSD, Linux, Unix, or Mac OS X system can use this process to connect to your machine.

Users on desktop client systems such as Windows or classic Mac OS have a little bit more work to do. These platforms have no command-line SSH client programs, but there are some excellent graphical terminal programs that incorporate both Telnet and SSH functionality: Windows users have SecureCRT (from Van Dyke, http://www.vandyke.com) or SSH (from SSH Communications Security, http://www.ssh.com), and Mac OS 9 users can use NiftyTelnet/SSH or MacSSH. The Windows programs tend to be commercial products, whereas most of the Mac programs are shareware.

Your task lies in convincing your users to switch to SSH rather than using Telnet. Let them all know via your published server policy that they are advised to use SSH to protect themselves at their option; however, this doesn't guarantee they will use it, and you as the administrator are still faced with the threat of an attacker who sniffs the connection of someone who has chosen not to use SSH. A more heavy-handed but complete approach is to disable Telnet entirely and require your users to use SSH instead. To disable Telnet, comment out the telnetd line from /etc/inetd.conf:

```bash
# telnet stream tcp nowait root /usr/libexec/telnetd telnetd
```

Then, restart the inetd process:

```bash
# killall -HUP inetd
```

> **NOTE**
> SSH has two popular protocol flavors: SSH1 and SSH2. FreeBSD supports both, but SSH1 is less well designed and potentially more likely to exhibit security vulnerabilities than SSH2. You can disable SSH1 by adding the following line to /etc/ssh/sshd_config:
>
> ```bash
> Protocol 2
> ```
>
> However, note that not all consumer SSH clients have full support for SSH2. Don't worry about disabling SSH1 unless you have to.

## Securing E-mail Services (POP3 and IMAP)

POP3 and IMAP are arguably even more vulnerable to clear-text security risks than Telnet. If your users have set their e-mail clients to connect to the server every five minutes or so to check for new messages, a plainly visible login and password transaction occurs with each one of these connections, resulting in an even higher likelihood of password compromises—especially because these services send their sensitive data at predictable, regular intervals. If you're enforcing SSH rather than Telnet on your server, it's in your interest to do the same for your e-mail services.

You learned in Chapter 25 how to secure the Qopop program to use the built-in Secure Sockets Layer (SSL) tools in FreeBSD to encrypt POP3 connections. You can use the same method to secure IMAP, employing the IMAP-UW software package. You can enable SSL support in IMAP-UW by generating a certificate with a Certifying Authority (as you learned in “Enabling SSL Encryption,” in Chapter 24). If you have a certificate generated for a different service (Qopop, for example) on your site, you can use the same certificate for IMAP-UW. Refer to the IMAP-UW documentation at http://www.washington.edu/imap/ for more details.

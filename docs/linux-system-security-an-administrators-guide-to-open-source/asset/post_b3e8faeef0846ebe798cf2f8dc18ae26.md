
# Redhat Linux Security

To subscribe, mail linux-security-request@redhat.com with subscribe in the subject of the message.

# rootshell Mailing List

Announcements and exploits of UNIX vulnerabilities.

To subscribe, mail majordomo@rootshell.com with subscribe announce in the subject of the message.

rootshell mailing list archives are at http://www.rootshell.com/mail-inglist-archive

# RPM Mailing List

Excellent list; recommended.

To subscribe, mail rpm-list-request@redhat.com with subscribe in the subject of the message.

# SANS Network Security Digest

Monthly newsletter highlighting recent vulnerabilities and providing security references for more information.

To subscribe, mail digest@sans.org with subscribe network security digest in the subject of the message.

# security-audit Mailing List

This list is for discussion of the auditing and hardening of the security of the Linux OS in a more systematic way. Not for exploits.

To subscribe, mail security-audit@subscribe@ferret.lmh.ox.ac.uk.

# Sneakers Mailing List

Firewalls and general security. Reserved for lawful tests and techniques.

To subscribe, mail Sneakers-Request@CS.Yale.EDU with subscribe in the subject of the message.

# SSH Users Mailing List

For users of ssh.

To subscribe, mail majordomo@clinet.fi with subscribe ssh in the subject of the message.

# sudo Mailing List

Mailing list for users of sudo.

To subscribe, mail majordomo@cs.colorado.edu with *subscribe sudo-users* in the subject of the message.

# SuSE Mailing List

Visit the home page for instructions on subscribing.

http://www.suse.com/Mailinglists/index.html

# TCFS Mailing List

For users of the Transparent Cryptographic File System.

tcfslist@mikonos.dia.unisa.it

To subscribe, mail *tiger-request@net.tamu.edu* with *subscribe* in the subject of the message.

# tiger Mailing List

Questions, answers, and announcements about the *tiger* auditing tool.

To subscribe, mail *tiger-request@net.tamu.edu* with *subscribe* in the subject of the message.

# USENET NEWSGROUPS

- comp.mail.sendmail
- comp.os.linux.networking
- comp.os.linux.security
- comp.security.ash
- comp.security.unix

## Tools Not Covered

There are a lot of good tools out there, but we didn’t have time to write about everything. Here we provide references to some of the tools we thought you might want to check out on your own.

### AAFID (Autonomous Agents for Intrusion Detection)

Eugene Spafford & Diego Zamboni

A set of small tools and an infrastructure that can be used to provide distributed monitoring and intrusion detection on a network of hosts. The code is written in Perl 5.

Home page:

http://www.cs.purdue.edu/coast/projects/autonomous-agents.html

FTP site:

ftp://coast.cs.purdue.edu/pub/COAST/tools/AAFID/

### FreeSwan

Team Effort.

Free version of Secure Wide Area Networking, provides IPsec and IKE for Linux. FreeSwan provides authentication and encryption services, enabling you to build virtual private networks. This allows you to create secure communications over an insecure network. Learn more at

```
http://www.xs4all.nl/~freeswan/
```

### fwconfig

Sonny Parlin  
Provides a GUI front-end to writing `ipchains` rules.

```
http://www.mindstorm.com/~sparlin/fwconfig.html
```

### FWTk (Firewall Toolkit)

Network Associate's commercial firewall designed to run on UNIX systems.

```
http://www.tis.com/research/software/
```

### Mason

William Sterns wrote this tool that helps you interactively generate firewall rules dynamically.

```
http://users.dhp.com/~whisper/mason/
```

### Merlin

Created by CIAC. Extensible GUI interface to security tools such as SPL-Net, tiger, COPS, Crack, and Tripwire. Written in Perl. Nice interface for reading reports produced by the tools.

```
http://ciac.llnl.gov/ciac/ToolsUnixSysMon.html#Merlin
```

### nessus

Renaud Deraison  
Modular port scanner for several varieties of UNIX.

```
http://www.nessus.org/
```

### netfilter

Rusty Russell  
Replacement for `ipchains` in kernel version 2.3.x.

```
http://www.rustcorp.com/linux/netfilter/
```

### nfsbug

Leendert van Doorn

C code to locate NFS misconfigurations and bugs that can lead to unauthorized access.

ftp://coast.cs.purdue.edu/pub/tools/unix/nfsbug/

### nfstrace

Matt Blaze

Toolkit for monitoring ethernet traffic and collecting NFS activity information.

ftp://coast.cs.purdue.edu/pub/tools/unix/nfstrace/

### nfswatch

David Curry and Jeff Mogul

Monitors and provides statistics on NFS traffic.

ftp://ftp.ers.ibm.com/pub/davy/

### nmap (Network Mapper)

Fyodor

Port scanner. Generates a variety of different types of packets (ICMP, UDP, TCP, ftp, etc.). Can be used to test your firewall.

http://www.insecure.org/

### SHADOW (Secondary Heuristic Analysis for Defensive Online Warfare)

Naval Surface Warfare Center

Intrusion detection software. Allows you to collect and analyze data with the help of tcpdump, libpcap, and configurable filters. Comes ready to recognize a variety of attack signatures.

http://www.nswc.navy.mil/SSEC/CID/

### SOCKSv5

SOCKSv5 is an industry standard (RFC1828). SOCKSv5 can be used to create a firewall.

http://www.socks5.nec.com/

### SLeay

Eric Young's Secure Socket Layer and supporting libraries.

ftp://ftp.psy.ug.oz.au/pub/Crypto/SSL/

# Glossary

**A**

- **acceptable use policy (AUP)** A policy describing expected behavior of a user who has an account on a system. AUPs may list activities that are specifically not allowed, such as distribution of unsolicited commercial e-mail, unauthorized access, etc., that may result in termination of the account.

**B**

- **bugtraq archive** The collection of messages previously sent to the bugtraq mailing list, a full-disclosure UNIX security list. See Appendix A.

**C**

- **C program** The C language is a popular systems programming language. It was originally developed by Ken Thompson and Dennis Ritchie.
- **CERT** An organization that can provide help recovering from or preventing computer intrusions.
- **Computer Security Institute (CSI)** A company that provides service and training for network, information, and computer security professionals.
- **CPU** Used to stand for central processing unit, now it can refer to one or more processors on a computer. Performs computations and controls other components of the computer.
- **Crack** A program designed to guess hashed UNIX passwords by iteratively generating a guess, hashing it, and comparing it to the target. If they match, the password has been guessed.
- **Cryptographic File System (CFS)** A filesystem on which the stored files are encrypted or decrypted once the user authenticates.

**D**

- **daemon** A program running in the background on a UNIX system, accepting requests on a port, named pipe, or UNIX domain socket, to provide some service.
- **DMZ** Demilitarized zone. One or more secured hosts that are logically between an internal network and external network. This is a protected area and an additional buffer to prevent unauthorized access.
- **DNS** Domain name service. A distributed, hierarchical system that exists to provide mapping between named items and typed data.
- **DSL** Digital subscriber line. Technology that allows faster transmission rates to be obtained over regular telephone lines.

**F**

- **Federal Bureau of Investigation (FBI)** Principal investigative arm of the U.S. Department of Justice. It can also provide services and training to other law enforcement agencies in the United States.
- **File Transfer Protocol (FTP)** Protocol used to transfer files from one computer to another.
- **Firewall** Used to restrict or prevent access from one computer system to another.
- **ftp** See File Transfer Protocol.

**G**

- **gecos field** A field in the password file containing information about the UID, such as the user’s name.
- **GNU** GNU’s Not UNIX. A Free Software Foundation project to produce a complete and freely available version of the UNIX operating system and utilities.
- **GPL** GNU General Public License. The copyright, it spells out the licensing details of GNU and other software distributed under the GPL.
- **graphical user interface (GUI)** Software that accepts input from a program displaying graphics and possibly accepting mouse input rather than from text on the command line.
- **group identification numbers (GID)** A number representing a particular UNIX group, used by the operating system and in programs. Usually /etc/ group provides a mapping between GIDs and group names.

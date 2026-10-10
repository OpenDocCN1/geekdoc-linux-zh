
For the rest of you, and if you're joining us again after installing Pcap, the next step to compile ARPWatch is to **make** it. From the command line within the ARPWatch source code directory, type this:

```
make
```

ARPWatch will now compile and you'll see messages indicating the progress, as well as possibly a warning or two:

```
report.o(.text+0x409): the use of 'mktemp' is dangerous, better use 'mkstemp'
gcc -O2 -DDPKG -DHAVE_FCNTL_H=1 -DHAVE_MEMORY_H=1 -DTIME_WITH_SYS_TIME=1 \
    -DHAVE_BCOP=1 -DHAVE_STRERROR=1 -DRETSTICTYPE=void -DRETSTIGVAL= \
    -DHAVE_SIGSET=1 -DDECLWAITSTATUS=int -DSTD_C_HEADERS=1 \
    -DARPDIR=\`/usr/local/arpwatch\` -DPATH \
    _SENDAI=\`/usr/sbin/sendmail\` -I\. \
    -Ilinux_include -c arpsnp.c
gcc -O2 -DDEBUG -DHAVE_FCNTL_H=1 -DHAVE_MEMORY_H=1 -DTIME_WITH_SYS_TIME=1 \
    -DHAVE_BCOP=1 -DHAVE_STRERROR=1 -DRETSTICTYPE=void -DRETSTIGVAL= \
    -DHAVE_SIGSET=1 -DDECLWAITSTATUS=int -DSTD_C_HEADERS=1 \
    -DARPDIR=\`/usr/local/arpwatch\` \
    -DPATH SENDAI=\`/usr/sbin/sendmail\` \
    -I. -Ilinux_include -c arpsnp.c
arpsnp.o db.o dns.o
report.c file.o into.o
report.o: in function 'report':
report.o(.text+0x409): the use of 'mktemp' is dangerous, better use 'mkstemp'
```

After it's compiled, install ARPWatch with the following command:

```
make install
```

ARPWatch will be installed (by default) into **/usr/local/sbin**. This directory is usually in root's path, but if you type **arpwatch** and receive a **command not found** error, you probably need to preface the command with its directory, like this:

```
/usr/local/bin/arpwatch
```

As ARPWatch runs, it will report to the SYSLOG daemon about new MAC addresses found on the network. This means that ARPWatch will usually output to **/var/log/messages**, so you can run a **grep** command to find out about the new hosts as ARPWatch finds them:

```
grep arpwatch /var/log/messages
```

Additionally, ARPWatch will also send email to the root account on a system detailing the new hosts as well. The email contains details such as the date, the IP address, and the MAC address:

```
hostname: client.example.com
ip address: 192.168.1.10
ethernet address: 0e1:18:34:2f:e8
ethernet vendor: <unknown>
timestamp: Saturday, May 22, 2004 11:25:59 -0500
```

In both of these ways, it's possible to know virtually instantly when a new host appears on the network. Such information would be helpful to the security administrator in monitoring for possible unauthorized use of a network.

ARPWatch will run in the background as a daemon, silently (or hopefully silently) going about its business and reporting back to you as needed. If, for some reason, ARPWatch shuts off, maybe due to the machine rebooting, the existing entries will be written to a file called `arp.dat` (the location of this file varies greatly; if you need to find it run `find / -name "arp.dat"`). If you need to reset ARPWatch's monitoring database so that it will "pick up" all the hosts on the network again, run these commands from within the directory in which you locate ARPWatch:

```
rm arp.dat
touch arp.dat
```

A tip about using ARPWatch: Make sure that the ARPWatch data file, `arp.dat`, is monitored for unauthorized changes. If an attacker can alter this file and add his own entry manually, ARPWatch won't alert you to the presence of the new host. Make sure that the `arp.dat` file is monitored by AIDE (covered in Chapter 12, "Filesystem Integrity") or through other similar means.

## Summary

This chapter showed you some of the tools used in intrusion detection. The goal was to provide you with some hands-on experience based on the concepts introduced in previous chapters. You learned about network sniffers in this chapter and focused specifically on TCPDump. Some packets and attack types were viewed through the eyes of TCPDump as well. Other tools were introduced and discussed in this chapter as well. These included Snort, which provides an excellent intrusion detection system. Finally, using ARPWatch to monitor for new and unexpected ARP entries on the network was also discussed. The next chapter looks at filesystem integrity through the eyes of AIDE, a filesystem integrity checker.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_398_0.png)

## Filesystem Integrity

Integrity is one of three commonly used principles of computer security; confidentiality and availability are the other two. In the purest sense of the three principles, integrity simply refers to the means by which you ensure that data is authentic and has not been altered or tampered with in any way. One aspect of ensuring data integrity is ensuring the integrity of the system on which the data is housed.

This chapter looks at some very specific means you have at your disposal when running Linux to ensure data integrity. These include examining the files on a Linux system to make sure that they haven’t been altered without your knowledge, and they include looking for anomalies that may indicate the presence of an intruder on the system.

### Filesystem Integrity Defined

Maintaining system integrity is yet another layer of security meant to give you, the security administrator, a warm, fuzzy feeling. For the purposes of this chapter, the term filesystem integrity refers to the verifiable knowledge that the computer system and the objects contained therein are in a known-good state. Although that’s a wide definition, filesystem integrity in this chapter will simply entail verification that the files located on the computer have not been tampered with or altered. As such, this chapter concentrates on tools to assist you in checking the files.

### Practical Filesystem Integrity

Various tools are available to check the integrity of files on the system. Tripwire is a commercial offering in the area that’s now been open sourced. Well, it was open source and then closed and now open, or something entirely too confusing. See Chapter 10, “Intrusion Detection Tools,” for a description of Tripwire’s licensing issues. In this chapter, I’ll show AIDE, the Advanced Intrusion Detection Environment. AIDE is an open-source filesystem integrity-checking tool.

A basic integrity check of a file usually involves obtaining checksum values of the files on the computer and comparing that checksum against a known-good value. Checksums are sometimes also referred to as hash values or signatures. More complex checking is done by tools such as AIDE, as you’ll see later in the chapter.

Checksums are frequently used to verify the integrity of a downloaded file. For example, many Linux FTP repositories contain a file called **md5sums**. Inside of that **md5sums** file are the checksums of the files as they reside on the FTP server. When you download the file, you can then run a checksum against the downloaded file. If your checksum value matches the checksum on the server, you know you have a good file. If the values don’t match, something went wrong with the download and you can save some time rather than trying to work with a corrupt file or wasting a CDR.

A hands-on example would be helpful. Jump into a console and type the following:

```
md5sum /etc/passwd
```

You’ll see a value such as this:

```
fc8053d1be0dcc33e8e6f264e8b8e502 /etc/passwd
```

Note that your value will be substantially different from mine, unless you’re running the command against my password file, in which case I have other problems that need attention.

If you add a user, delete a user, or make any change that affects the password file, that **md5sum** value will change. For example, if you make a change to someone’s name within the **passwd** file, the **md5sum** of the **passwd** file will change because the file’s contents are now different.

Continuing with the preceding example, you can change the name of the root user by running this (as root):

```
chfn root
```

You’ll be presented with various options for changing the account information for the user, beginning with the Full Name. Change the Full Name value to whatever you’d like, and continue with changes to other values if you’d like. Now running an **md5sum** against **/etc/passwd** will show a different checksum for the file:

```
md5sum /etc/passwd
5a916699b172ab44c75bbf2d2582849bf /etc/passwd
```

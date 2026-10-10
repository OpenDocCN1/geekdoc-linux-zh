
# Chapter 11

## DHCP

This document attempts to answer basic questions on how to set up your Linux box to serve as a DHCP server or a DHCP client.

DHCP, the Dynamic Host Configuration Protocol, is commonly used on Ethernet and Ethernet-like networks to automatically give hosts an IP address and network address information at startup (a host needs this information to communicate over an Internet). Typically, the assigned IP address will expire after a time, and the host will have to request a new address when its current IP address expires; hence the dynamic in DHCP.

Very small networks seldom bother with DHCP, but larger networks in offices and towns often do use it. If your Linux host is part of a corporate network or you'll be plugging into a cable modem network, you may need to run a DHCP client. This chapter will tell you how.

Similarly, if you operate a medium- or large-sized network yourself, you may want to run a DHCP server to assign IP addresses to your hosts. This will save you some legwork, especially when hosts move around. This chapter will tell you how to do so.

This chapter is reprinted from the DHCP mini-HOWTO, version 2.6 of 14 November 1998, by Vladimir Vuskan.

### INTRODUCTION

This introductory section contains general information for this chapter and contact information for the author.

### Standard Disclaimer

No liability for the content of this chapter can be accepted. Use the concepts, examples, and other content at your own risk. As this is a new edition of this document, there may be errors and inaccuracies, which may, of course, be damaging to your system. Proceed with caution, and although damage is highly unlikely, I won't take any responsibility for it if it does occur.

Also bear in mind that this is not official information. Much of the content in this chapter is based on assumptions, which appear to work for people. Use the information at your own risk.

### New Versions of This Document

New versions of this document will be periodically posted to comp.os.linux.answers. They will also be added to the various anonymous FTP sites that archive such information, including ftp://MetaLab.unc.edu/pub/linux/docs/HOWTO

In addition, you should generally be able to find this document on the Linux Documentation Project page via http://MetaLab.unc.edu/LDP/.

### Feedback

Feedback is most certainly welcome for this document. Without your submissions and input, this document wouldn't exist. So, please post your additions, comments, and criticisms to **vukasan@veus.hr**.

### Contributors

This chapter has been modified from the original version by Paul Makeev.

The following people have contributed to this mini-HOWTO.

- Heiko Schittertermann
- Jonathan Smith
- Dan Khabaza
- Hal Sadofsky
- Henrik Stoerner
- Paul Rossington

### Copyright Information

This document is copyrighted ©1998 Vladimir Vukan and distributed under the following terms:

- Linux HOWTO documents may be reproduced and distributed in whole or in part, in any medium—physical or electronic, as long as this copyright notice is retained on all copies. Commercial redistribution is allowed and encouraged; however, the author would like to be notified of any such distributions.
- All translations, derivative works, or aggregate works incorporating any Linux HOWTO documents must be covered under this copyright notice. That is, you may not produce a derivative work from a HOWTO and impose additional restrictions on its distribution. Exceptions to these rules may be granted under certain conditions; please contact the Linux HOWTO coordinator at the address given below.
- If you have questions, please contact the Linux HOWTO coordinator at `linux-howto@MetaLab.unc.edu`.

![](img/a3584dae761d2e3abed8bf40d7637389_410_0.png)

### DHCP

DHCP is Dynamic Host Configuration Protocol. It is used to control vital networking parameters of hosts (running clients) with the help of a server. DHCP is backward compatible with BOOTP. For more information, see RFC 2131 (old RFC 1531). (See Internet Resources section at the end of the document). You can also read DHCP FAQ (`http://web.syr.edu/~jmwebus/compfaqs/dhcp.faq.html`).

This mini-HOWTO covers both the DHCP server daemon as well as DHCP client daemon. Most people need the client daemon, which is used by workstations to obtain network information from a remote server. The server daemon is used by system administrators to distribute network information to clients, so if you are just a regular user, you need the client daemon.

### Client Setup

This section details setting up and troubleshooting the DHCP client daemon on different distributions of Linux.

#### Downloading the Client Daemon

- **2.0.x kernels** No matter what distribution you are using, you will need to download the DHCP client daemon for Linux. The package you need to download is called `dhcpd` and the current version is 0.70. You can read the description of the package at `ftp://metalab.unc.edu/pub/Linux/system/network/daemons/dhcpd-0.70.lsm`.
- **2.1.x kernels** Because of changes in the IPv4 network package in 2.1.x kernels (e.g., the way it sets the defaults for several fields) dhcpd doesn't work properly. Most users don't run experimental kernels, so this shouldn't be a problem. If you do, you should try dhcpd 1.3.16, which is a modified version written by Sergei Viznyuk `<sergei@phystech.com>`. You can fetch it at:
  - `http://phystech.dyn.ml.org/pub/`
  - `http://www.cps.msu.edu/~dunham/out/dhcpd-1.3.6.tar.gz`

### Slackware

You can download the latest copy of the dhcpd from any Sunsite mirror or the following:

- ftp://ftp.cdrom.com/pub/linux/sunsite/system/network/daemons/
- ftp://MetaLab.unc.edu/pub/Linux/system/network/daemons
- ftp://ftp.kobe-u.ac.jp/pub/PC-UNIX/Linux/network/dhcpd (Primary site in Japan)

Once you've downloaded the latest version of dhcpd.tar.gz, follow these steps:

1. Unpack it: `tar -zxvf dhcpd-0.70.tar.gz`.
2. Cd into the directory and make dhcpd: `cd dhcpd-0.70` and `make`
3. Install it (you have to run the following command as root): `make install`

This will create the directory /etc/dhcpc, where dhcpd will store the DHCP information, and the dhcpd file will be copied into /usr/sbin.

In order to make the system initialize using DHCP during boot, type the following:

```sh
cd /etc/rc.d
mv rc.inet1 rc.inet1.OLD
```

This will move the old network initialization script into rc.inet1.OLD. You now need to create the new rc.inet1 script. The following code is all you need:

```sh
#!/bin/sh

# rc.inet1   This shell script boots up the base INET system.

HOSTNAME=`cat /etc/HOSTNAME`  #This is probably not necessary #but I will leave it in anyways

# Attach the loopback device.
/sbin/ifconfig lo 127.0.0.1
/sbin/route add -net 127.0.0.0 netmask 255.0.0.0 lo

# IF YOU HAVE AN ETHERNET CONNECTION, use these lines below
# to configure the eth0 interface. If you're only using
# loopback or SLIP, don't include the rest of the lines in
# this file.

/usr/sbin/dhcpd
```

Save it and reboot your computer.

When you are finished, go to the “Tying It All Together” section.

### Red Hat 5.x

dhcpd configuration under Red Hat 5.0+ is really easy. All you need to do is start the Control Panel by typing **control-panel**. Then follow these steps:

1. Select “Network Configuration”.
2. Click Interfaces.
3. Click Add.
4. Select Ethernet.
5. In the Edit Ethernet/Bus Interface select “Activate interface at boot time”, as well as DHCP as “Interface configuration protocol”.

When you are finished, go to the “Tying It All Together” section.

### Red Hat 4.x and Caldera OpenLinux 1.1/1.2

dhcpd is included in the standard Red Hat distribution as an RPM, and you can find it on your distribution’s CD-ROM in the RPMS directory or you can download it from

```text
ftp://ftp.redhat.com/pub/redhat/redhat-4.2/i386/RedHat/RPMS/
dhcpd-0.6-2.i386.rpm
```

and install it with `rpm -i dhcpd-0.6-2.i386.rpm`.

Alternatively you can compile your own version by following the steps outlined in the Slackware section.

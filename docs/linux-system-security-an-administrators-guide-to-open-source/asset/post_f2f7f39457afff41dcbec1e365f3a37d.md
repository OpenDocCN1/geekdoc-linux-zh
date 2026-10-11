
## Securing Network Services: TCP_wrappers, portmap, and xinetd

Which network services should be made available? That depends upon many aspects of your computing environment. The best place to begin is with your organization's Security Policy (see Chapter 2), which should establish the philosophy of either generally permitting services (everything is allowed except that which is expressly forbidden) or generally forbidding services (that which is not expressly permitted is denied). Which philosophy you implement will dictate your default behavior. For the balance of our discussion, we will assume the latter policy of denial by default, because it reflects a more secure perspective.

Once you have established the default policy, the next step depends upon individual system requirements. Some systems, for example, will act as network install servers and therefore will need to make available services such as bootpd, rarpd, and in.tftpd. Other systems may only need to provide typical services such as in.ftpd, in.telnetd, and sshd. Still other systems may need to provide NFS, NIS, electronic mail, and/or DNS services. In every case, once you have determined that a particular system needs to provide a specific service, you must determine which systems and users require the services and then configure those services so that only the required systems and users are allowed to access the service. But that's not all! You must then configure the services in such a way that they generate an appropriate amount of log detail. And then you need to read those log files! There is some help with the reading of the log files—we discuss that topic in Chapter 17.

We provide an overview of and references to the topic of network services in *TCP/IP Networking Overview* on page 28. In this chapter, we will consider ways to improve the security of those services so decide to use through the use of the access control lists and additional logging provided by TCP\_wrappers. Additionally, we will look at configuring the *portmap* daemon in a more secure way. Finally, we will consider *xinetd*, a replacement for *inetd*, which offers greater flexibility for securing the network services to be made available as well as protection against certain types of DoS attacks.

### TCP\_WRAPPERS

Almost all of the services provided through *inetd* are invoked through TCP\_wrappers by way of the TCP\_wrappers daemon, *tcpd*. TCP\_wrappers was written and continues to be maintained by Wietse Venema. It is included with many Linux distributions including Red Hat 5.2/6.0 and it runs on most flavors of UNIX. If you don't already have a copy, you can obtain one from *http://ftp.cert.org/pub/tools/tcp_wrappers/* (as well as various other sites throughout the Internet. Make sure that you pull it down from a site, like this one, that includes a digital signature. Then check the signature!)

The TCP\_wrappers software is distributable under the terms displayed in Example 10-1. In other words, it is publicly available! This notice is found in the *DISCLAIMER* file in the top directory of the source tree.

#### Example 10-1 TCP\_Wrappers Copyright Notice

```text
* Copyright 1995 by Wietse Venema.  All rights reserved.  Some individual
* files may be covered by other copyrights.
*
* This material was originally written and compiled by Wietse Venema at
* Eindhoven University of Technology, The Netherlands, in 1990, 1991,
* 1992, 1993, 1994 and 1995.
*
* Redistribution and use in source and binary forms are permitted
* provided that this entire copyright notice is duplicated in all such
* copies.
*
* This software is provided "as is" and without any expressed or implied
* warranties, including, without limitation, the implied warranties of
* merchantability and fitness for any particular purpose.
```

The TCP\_wrappers mechanism provides access control list restrictions and logging for all service requests to the service it wraps. It may be used for either UDP or TCP services as long as the service are invoked through a central daemon process such as *inetd*. This requirement is based on the nature of *tcpd*, the TCP\_wrappers daemon, which is invoked by *inetd* instead of the service being requested. This is due to appropriate entries in */etc/inetd.conf*, as shown in Example 10-2.

Notice that, for many of the services (some of which are commented out and therefore not available), the sixth field is */usr/sbin/tcpd* instead of the

#### Example 10-2 Default /etc/inetd.conf File in Red Hat Distributions

```text
# inetd.conf This file describes the services that will be available
# through the INETD TCP/IP super server. To re-configure
# the running INETD process, edit this file, then send the
# INETD process a SIGHUP signal.
#
# Version: @(#) /etc/inetd.conf 3.10 05/27/93
# Authors: Original taken from TASH UNIX 4.3/44BSD
# Fred N. van Kempen, <waltj@ewalt.nl.mugnet.org>
#
# Modified for Debian Linux by Ian A. Murdock <imurdo@ck.shell.portal.com>
# Modified for RSH Linux by Marc Ewing <marc@redhat.com>
#
<service_name> <sock_type> <proto> <flags> <user> <server_path> <args>
#
# Echo, discard, daytime, and chargen are used primarily for testing.
#
# To re-read this file after changes, just do a 'killall -HUP inetd'
#
#echo stream tcp nowait root internal
#echo dgram udp wait root internal
#discard stream tcp nowait root internal
#discard dgram udp wait root internal
#daytime stream tcp nowait root internal
#daytime dgram udp wait root internal
#chargen stream tcp nowait root internal
#chargen dgram udp wait root internal
#time stream tcp nowait root internal
#time dgram udp wait root internal
# These are standard services.
#
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd -l -a
# telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
#
# Shell, login, exec, comsat and talk are BSD protocols.
#
#shell stream tcp nowait root /usr/sbin/tcpd in.rshd
#login stream tcp nowait root /usr/sbin/tcpd in.logind
#exec stream tcp nowait root /usr/sbin/tcpd in.rexecd
#comsat dgram udp wait root /usr/sbin/tcpd in.comsat
#talk dgram udp wait root /usr/sbin/tcpd in.talkd
#ntalk dgram udp wait root /usr/sbin/tcpd in.ntalkd
#dtalk stream tcp waity nobody /usr/sbin/tcpd in.dtalkd
#
# Pop and imap mail services et al
#
#pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
#pop-3 stream tcp nowait root /usr/sbin/tcpd pop3d
#imap stream tcp nowait root /usr/sbin/tcpd imapd
#
# The Internet UUCP service.
#
#uucp stream tcp nowait uucp /usr/sbin/tcpd /usr/lib/uucp/uucico -l
#
# ttyd service is provided primarily for booting. Most sites
# run this only on machines acting as "boot servers". Do not uncomment
# this unless your 'need' it.
#
#tftp dgram udp wait root /usr/sbin/tcpd in.tftpd
#bootps dgram udp wait root /usr/sbin/tcpd bootpd
#
# Finger, systat and netstat give out user information which may be
# valuable to potential *system crackers.* Many sites choose to disable
# some or all of these services to improve security.
#
#fingr stream tcp nowait root /usr/sbin/tcpd in.fingerd
#cfinger stream tcp nowait root /usr/sbin/tcpd in.cfingerd
#systat stream tcp nowait guest /usr/sbin/tcpd /bin/ps -auxw
#netstat stream tcp nowait guest /usr/sbin/tcpd /bin/netstat -f inet
#
# Authentication
#
auth stream tcp nowait nobody /usr/sbin/in.inetd in.inetd -l -e -o
# End of inetd.conf

linuxconf stream tcp wait root /bin/linuxconf linuxconf --http
#swat stream tcp nowait.400 root /usr/sbin/swat swat
```

daemon. Therefore, when a service with such an entry—like telnet—is requested by a client, inetd will invoke tcpd instead.

Basically, whenever a client requests a service, it will be invoked either through inetd or through the portmap daemon (RPC services only), or a server daemon will already be running. Server daemons that are run all the time (such as rpc.mountd) will be invoked at boot time through a start-up script (/etc/rc, in/init, d/nfs in the case of rpc.mountd) or started manually. Otherwise, in order for a service to be available on a server, you will find an entry in /etc/inetd.conf for management by inetd or in /etc/rpc for RPC services managed by portmap. For a thorough treatment of TCP/IP services in general, see the references cited in General TCP/IP Networking Resources on page 39 in Chapter 3.

This means that the functionality provided by tcpd is separate from any service being requested. Therefore, to get similar functionality into a daemon that is always bound to a port, such as syslogd -r (discussed in Chapter 8), the bound daemon would have to be rewritten for that purpose (Wietse Venema did exactly that for the portmap daemon which is discussed in The Port-mapper on page 218). Figure 10.1 provides an overview of the flow of an initial request to a server in the presence of TCP_wrappers.

As is shown in the figure, TCP_wrappers performs a few simple but very important tasks. It checks the access control list to determine whether a connection should be allowed and submits a log entry to syslogd. If the access list allows the service, tcpd invokes the appropriate daemon, which then proceeds with its own authentication mechanism (if applicable) and may write its own message to syslogd.

### Building TCP_Wrappers

If you are using a version of Linux (or UNIX, for that matter) that does not include TCP_wrappers as part of the distribution (unlike Red Hat 5.2/6.0), you will need to compile and link the various programs. Even if you are using Red Hat 5.2/6.0, you may decide that you need to recompile TCP-wrappers with


This listing sets the host as a slave nameserver. If the master nameserver goes down, this one will pick up the activity. Compare the following code:

```text
zone " "."in" {
    type hint;
    file "root.cache";
};
```

This defines the root nameserver cache. The root.cache file keeps name address translations for the top-level domains.

```text
zone "0.0.127.in-addr.arpa" in {
    type master;
    file "named.local";
};
```

This defines the localhost network. It is always the 127.0.0.0 network.

## Configuring a Linux Host

When you have your network card installed and support for it enabled (you'll have to recompile the kernel), you'll need to configure your network. To configure your network configuration files, run `/sbin/netconfig`. Doing so runs a script that prompts you for information. Make sure you already have the following vital info from your network administrator:

- IP address (if needed)
- Primary Name Server
- Secondary Name Server
- Gateway
- Domain name
- Hostname
- Netmask (also known as a subnet mask)

Run `/sbin/netconfig`. Hit Enter to start the network configuration, shown in Figure 11-1.

![](img/8ad518fddafc7f5e73715a2604b61d50_371_0.png)

The following prompts appear. Enter the information as suggested.

1. For ENTER HOSTNAME, enter your hostname (in all lowercase) then press Enter. See Figure 11-2.

![](img/8ad518fddafc7f5e73715a2604b61d50_371_1.png)

2. For ENTER DOMAIN NAME, enter `company.com` and then press Enter. (See Figure 11-3.) Replace `company` with your real company name.

![](img/8ad518fddafc7f5e73715a2604b61d50_371_2.png)

3. For LOOPBACK ONLY, press Tab until you get to No, and then press Enter. (See Figure 11-4.)

![](img/8ad518fddafc7f5e73715a2604b61d50_372_0.png)

4. For ENTER LOCAL IP ADDRESS, type your IP address, and then press Enter. If your network uses DHCP instead of static addresses, you can enter "1.1.1.1" instead. (See Figure 11-5.)

![](img/8ad518fddafc7f5e73715a2604b61d50_372_1.png)

5. For ENTER GATEWAY ADDRESS, type your gateway address, and then press Enter. (See Figure 11-6.)

![](img/8ad518fddafc7f5e73715a2604b61d50_372_2.png)

6. For ENTER NETMASK, type your netmask, and then press Enter. It will look something like 255.255.255.0 or 255.255.248.0. (See Figure 11-7.)

![](img/8ad518fddafc7f5e73715a2604b61d50_373_0.png)

Figure 11-7: Setting your netmask

7. For USE A NAMESERVER, press Enter to default to YES; otherwise you're going to get really tired of typing in IP numbers. (See Figure 11-8.)

![](img/8ad518fddafc7f5e73715a2604b61d50_373_1.png)

Figure 11-8: Setting your nameserver

8. For SELECT NAMESERVER, type your nameserver IP address (not the name), and then press Enter. (See Figure 11-9.)

![](img/8ad518fddafc7f5e73715a2604b61d50_373_2.png)

Figure 11-9: Viewing your final screen

9. Press Return or Enter on your final screen, and now you're done with your host configuration. Be sure to reboot to take full advantage of your networking capabilities (if you don't reboot, they can't take effect).

## Examining Network Daemons

There are all sorts of network daemons: `telnetd`, `sshd`, `ftpd`, `tftpd`. When a socket is open for an application, the daemon sits on the application's socket and waits for a connection. When the socket is closed for that application, the daemon stops.

Daemons don’t run on their own, they are controlled by inetd, which is a super-daemon. The inetd configuration file can affect which applications and protocols can be run, and can even enable logging on some applications. So you can think of inetd as a socket manager.

When inetd runs, it reads the configuration file. If you update this file, give inetd the hangup signal (`kill –HUP <processid>`). This causes inetd to reread the `/etc/inetd.conf` file.

Note the permissions on `/etc/inetd.conf`:

```text
$ ls –l /etc/inetd.conf
-rw-r-r-- 1 root root 4998 Oct 15 1997 /etc/inetd.conf
```

You never want this file to have any more permissions than 644! This keeps users from writing to the `/etc/inetd.conf` file.

An entry in `/etc/inetd.conf` is formatted like this:

```text
service_name sock_type proto flags user server_path args
```

FTP is a good example of all the syntax usage.

```text
Ftp stream tcp nowait root /usr/sbin/tcpd wu.ftp –l –i –a
```

Here FTP is defined as the service (as in the `/etc/services` file). It uses a data stream (you’ll also see a dgram, which is short for datagram, on UDP packets). It uses TCP for the transport protocol, and the information is sent via stream—it could also be a datagram as well as a number of other packets. The nowait means that the protocol does not wait to free the socket (this only applies to datagram packets), and the ftpd runs as user root.

The daemon that actually runs is wu.ftp, which is the WUarchive FTP daemon. Option –l (lowercase L) turns on the logging option.

Take a look at the entire `/etc/inetd.conf` file, shown in Listing 11–1.

### Listing 11–1: /etc/inetd.conf file

```text
# more /etc/inetd.conf
# See "man 8 inetd" for more information.
#
#
# If you make changes to this file, either reboot your machine or send the
# inetd a HUP signal:
# Do a "ps x" as root and look up the pid of inetd. Then do a
# "kill –HUP <pid of inetd>".
# The inetd will re-read this file whenever it gets that signal.
#
# <service_name> <sock_type> <proto> <flags> <user> <server_path> <args>
#

# The first 4 services are really only used for debugging purposes, so
# we comment them out since they can otherwise be used for some nasty
# denial-of-service attacks. If you need them, uncomment them.
# echo stream tcp nowait root internal
# echo dgram udp wait root internal
# discard stream tcp nowait root internal
# discard dgram udp wait root internal
# daytime stream tcp nowait root internal
# daytime dgram udp wait root internal
# chargen stream tcp nowait root internal
# chargen dgram udp wait root internal
time stream tcp nowait root internal
time dgram udp wait root internal
#
# These are standard services.
#
ftp stream tcp nowait root /usr/sbin/tcpd wu.ftp -1 -i -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
#

# Use this one instead if you want to snoop on telnet users (try to use this
# for ethical purposes, ok folks?):
# telnet stream tcp nowait root /usr/sbin/tcpd
/usr/sbin/in.telnetd
#

# This is generally unnecessary. The daemon provided by INN will handle the
# incoming NNTP connections.
# nntp stream tcp nowait root /usr/sbin/tcpd in.nttpd
#

# This is for BSD sendmail. NOTE: It's not a good idea to uncomment this
# one, since sendmail is already set up to run as a daemon in /etc/rc.d/rc.M.
# But, If you really want to run sendmail this way for some reason, you'll
# need to uncomment the smtp line following AND change the line in
/etc/rc.d/rc.M
# to run sendmail like this: /usr/sbin/sendmail -q30m
# ...otherwise the queue will not be processed.
# smtp stream tcp nowait root /usr/sbin/tcpd sendmail -bs

# The comsat daemon notifies the user of new mail when biff is set to y:
comsat dgram udp wait root /usr/sbin/tcpd in.comsat
#

# Shell, login, exec and talk are BSD protocols.
#
shell stream tcp nowait root /usr/sbin/tcpd in.rshd -L
login stream tcp nowait root /usr/sbin/tcpd in.rlogind
# exec stream tcp nowait root /usr/sbin/tcpd in.rexecd
# talk dgram udp wait root /usr/sbin/tcpd in.talkd
ntalk dgram udp wait root /usr/sbin/tcpd in.ntalkd
# 
# Kerberos authenticated services 
# 
# klogin stream tcp nowait root /usr/sbin/tcpd rlogind -k 
# eklogin stream tcp nowait root /usr/sbin/tcpd rlogind -k -x 
# kshell stream tcp nowait root /usr/sbin/tcpd rshd -k 
# 
# Services run ONLY on the Kerberos server 
# 
# krbupdase stream tcp nowait root /usr/sbin/tcpd registerd 
# kpasswd stream tcp nowait root /usr/sbin/tcpd kpasswd 
# Pop et al 
# 
pop2 stream tcp nowait root /usr/sbin/tcpd in.pop2d 
pop3 stream tcp nowait root /usr/sbin/tcpd in.pop3d 
# The ipop3d POP3 server is part of the Pine distribution. If you've 
# installed the Pine package, you may wish to switch to ipop3d by 
# commenting out the pop3 line above, and uncommenting the ipop3d line following.
#ipop3 stream tcp nowait root /usr/sbin/tcpd ipop3d 
imap2 stream tcp nowait root /usr/sbin/tcpd imapd 
# 
# The Internet UUCP service. 
# 
# uucp stream tcp nowait uucp /usr/sbin/tcpd /usr/lib/uucp/uucico -l 
# 
# Tftp service is provided primarily for booting. Most sites 
# run this only on machines acting as "boot servers." 
# 
# tftp dgram udp wait nobody /usr/sbin/tcpd in.tftp 
# bootps dgram udp wait root /usr/sbin/in.bootpd in.bootpd 
# 
# Finger, systat and netstat give out user information which may be 
# valuable to potential "system crackers." Many sites choose to disable 
# some or all of these services to improve security. 
# Try "telnet localhost systat" and "telnet localhost netstat" to see that 
# information yourself! 
#
finger stream tcp nowait nobody /usr/sbin/tcpd in.fingerd -w 
systat stream tcp nowait nobody /usr/sbin/tcpd /bin/ps -auwx 
netstat stream tcp nowait root /usr/sbin/tcpd /bin/netstat -a 
#
```

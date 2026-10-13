
# rotate, starting with the oldest log
if [ -f $back3 ] ; then
mv -fv $back3 $back4
fi
if [ -f $back2 ] ; then
mv -fv $back2 $back3
fi
if [ -f $back1 ] ; then
mv -fv $back1 $back2
fi
if [ -f $name ] ; then
mv -fv $name $back1
fi
touch $name; echo chmod 0600 $name
done

exit 0

4. That'll do what we want. Let's see what happens when we run this:

```
# rotatelogs.sh
'lastlog' -> 'lastlog.1'
chmod 0600 lastlog
'maillog.3' -> 'maillog.4'
'maillog.2' -> 'maillog.3'
'maillog.1' -> 'maillog.2'
'maillog' -> 'maillog.1'
chmod 0600 maillog
'wtmp.1' -> 'wtmp.2'
'wtmp' -> 'wtmp.1'
chmod 0600 wtmp
'error_log' -> 'error_log.1'
chmod 0600 error_log
'dmesg' -> 'dmesg.1'
chmod 0600 dmesg
'cron.3' -> 'cron.4'
'cron.2' -> 'cron.3'
'cron.1' -> 'cron.2'
'cron' -> 'cron.1'
chmod 0600 cron
'rpmpkgs.3' -> 'rpmpkgs.4'
'rpmpkgs.2' -> 'rpmpkgs.3'
'rpmpkgs.1' -> 'rpmpkgs.2'
'rpmpkgs' -> 'rpmpkgs.1'
chmod 0600 rpmpkgs
'./httpd/error_log.3' -> './httpd/error_log.4'
'./httpd/error_log.2' -> './httpd/error_log.3'
'./httpd/error_log.1' -> './httpd/error_log.2'
'./httpd/error_log' -> './httpd/error_log.1'
chmod 0600 ./httpd/error_log
'./httpd/access_log.3' -> './httpd/access_log.4'
'./httpd/access_log.2' -> './httpd/access_log.3'
'./httpd/access_log.1' -> './httpd/access_log.2'
'./httpd/access_log' -> './httpd/access_log.1'
chmod 0600 ./httpd/access_log
```

Voila! The final step is to drop this into the appropriate cron file or directory, set it to run weekly, and we're done.

There are some refinements you could make to this script, most notably having the log files compressed with gzip, but in general, this will do a nice job of rotating all the log files on a given Unix system. Note that not all Unices support the -v flag to mv, however, so you might have to chop that out before your script runs correctly.

## Q&A

**Q:** As it's impossible to document all possible Unix log files in this book, how do I figure out what program creates a given log file on my Unix system?

**A:** Usually, the log file corresponds to the name of the program, which makes it easy (for example, syslogd.log for syslog, ftpd.log for ftp). If not, man -k is a smart way to look. You can also strip a trailing d if there is one.

**Q:** Tracking hackers seems quite interesting. How often does it produce positive results?

**A:** Well...the reality is that it's very unlikely that you'll accomplish anything meaningful. On the other hand, if we don't try to notify administrators of malicious users, it certainly won't improve things.

## Workshop

### Quiz

1. What are the two primary reasons to pay attention to your log files?
2. What's in the messages log file, and what is it commonly called on other Unix systems?
3. Using the tips suggested in this hour, what's in ksyms on a Linux system?
4. What's the basic technique for the reverse lookup of an IP address to ascertain its domain?
5. Earlier in the hour, we analyzed the access_log file to figure out what domains were hitting our Web server. How would you modify that command to identify just the most popular top-level domains?

### Answers

1. Always pay attention to your log files so you are aware of attempted break-ins, and so you can keep track of disk space on your server.
2. The messages log file is used by syslogd, and on some systems it's called /var/log/syslog.
3. On a Linux box:

```
# man -k ksyms
gensyms                (8)  - generate symbol version information
ksyms                  (8)  - display exported kernel symbols
```

4. Use the host command and make sure you specify the -dv flags for maximal output (see the man page).
5. There are a couple of ways to accomplish this, but I really like using the rev command to reverse the domain name, cut the first field out, reverse it again, and do "the usual" sequence after that:

```
# awk '{print $1}' access_log | rev | cut -d . -f1 | rev | sort | \
uniq -c | sort -rn | head -10
2256 net
2198 com
579 es
348 us
339 pl
317 edu
311 249
228 ca
205 uk
198 55
```

In the next hour we'll move to a new topic—network configuration. We'll start with an exploration of IP addresses and netmasks, and then we'll look at the steps necessary to configure a Unix box to work on an Ethernet or PPP network.

![](img/5ced0c78d748bd190e9027e5549a3622_341_0.png)

## PART VI

### Network Topics

| Hour | Topic | Page |
|------|-------|------|
| 17 | Basic Network Configuration | 327 |
| 18 | Running Your Own Name Server | 353 |
| 19 | Running Internet Services | 373 |
| 20 | Working with E-mail | 391 |

## Hour 17

### Basic Network Configuration

![](img/5ced0c78d748bd190e9027e5549a3622_343_0.png)

It’s hard to imagine a computer, Unix or otherwise, that isn’t directly connected to the Internet. Whether via a direct LAN connection in an office, a high-speed home connection through a digital subscriber line (DSL) or cable modem, or, perhaps a modem/router combination to power your network, if you’re administering a Unix system, you need to know how to get it on—and keep it on—the Internet. Even if you’re still stuck with a modem.

That’s what the next few hours are all about. Starting with this first hour that explores how to hook a Unix system into an existing hard-coded IP or DHCP network, we’ll extend coverage in subsequent hours to include network services, domain name servers, and the complex but critical sendmail program.

In this hour, we’ll cover

- Connecting to the Internet using Linux
- Configuring your network with other Unixes
- Testing and evaluating connectivity

### Hooking Up a Linux Box to the Internet

Whether you're adding a Unix box to your existing network, or whether you're adding a Windows or Macintosh, there are two basic types of connections: hard-coded IP addresses and DHCP. Older facilities and those sites that have had complex networks for years often still run with fixed IP addresses for each system. In this scenario, you'll assign a unique, unused address within the available address range for each workstation or network device on the LAN.

This implies that your facility has either installed a proxy server that enables you to use IP addresses independent of the rest of the Internet¹, or your facility has either a Class B IP block or one or more Class C blocks. Each Class C block has 254 addresses, and each Class B block has more than 65,000 addresses.

![](img/5ced0c78d748bd190e9027e5549a3622_344_0.png)

> It's worth noting that an IP address block is .0 to .255, but that by convention .0 and .255 are reserved for loopback (a shorthand for your own system) and broadcast (a shorthand for all systems on the local network), and aren't assigned individual workstations or devices.

Much more common than fixed IP addresses is a dynamic IP assignment protocol. That's what the Point-to-Point Protocol (PPP) is, as used by America Online, Earthlink, and other ISPs. Within a LAN, however, PPP proves less efficient than the alternative, the Dynamic Host Configuration Protocol (DHCP).

### Task 17.1: Hooking Up a Linux System

If you are running DHCP, the job of hooking a new system up to the network is a breeze: The only task required is to specify DHCP as the connection choice during the initial installation of the operating system.

Hard-coded IP systems are a bit more tricky to configure. There are six essential numbers you'll need: the new system IP address, the netmask, the gateway (or router) address for the new system (which will vary depending on which subnet the system is connected into), a network and broadcast address, and at least one domain name system (DNS) server address.

1. If you're unsure whether your Linux box is trying to connect to the Internet via DHCP or a fixed IP, the place to look on a Red Hat system is in `/etc/sysconfig`. First off, make sure you've enabled networking in the first place by looking in `network`:

```
# cat /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=sombrero.dsldesigns.net
```

This is also where the hostname is set. Make sure you specify a full domain path here, rather than just the basic hostname. Or not...(see the Caution).

![](img/5ced0c78d748bd190e9027e5549a3622_345_0.png)

> The contents of the network file is a fine example of the divergence of standardization even within the Linux world: Red Hat encourages sysadmins to use the hostname and not the domain name; SuSE Linux uses the hostname, and has a separate variable (in /etc/rc.local, just like Mac OS X) called FQHOSTNAME for the hostname and domain together; and Mandrake has two variables in its configuration file, HOSTNAME and DOMAINNAME. Pay attention to the configuration material included with your Linux system to ensure that you set yours correctly if you're changing things post-installation!

The details of how the system talks with the rest of the network is contained within the interface configuration file for the specific interface. Most likely, the system uses eth0 as the default Ethernet configuration, so the configuration file in question is /etc/sysconfig/network-scripts/ifcfg-eth0:

```
# cat ifcfg-eth0
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
TYPE=Ethernet
USERCTL=no
PEERDNS=no
NETWORK=0.0.0.0
BROADCAST=255.255.255.255
```

![](img/5ced0c78d748bd190e9027e5549a3622_345_1.png)

> Remember the filename mnemonic here: if = interface, and cfg = config, so ifcfg-eth0 is the interface configuration file for the eth0 Ethernet connection.

Most of the fields in this file are unnecessary on a system that's using DHCP, but the critical one to eyeball is BOOTPROTO. If that's DHCP, as we see here, the system kicks off a program called the DHCP client daemon (dhcpcd) that manages the client-side DHCP interaction.

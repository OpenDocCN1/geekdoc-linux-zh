
After you have enabled dial-on-demand, you can create a startup script to automatically start the `pppd` daemon each time your system boots. There are several ways to do this; but, as you have seen in Chapter 11, “System Configuration and Startup Scripts,” the best way is to create a startup script in `/usr/local/etc/rc.d` with the single line `pppd` in it. This file can be called anything you want, but it’s a good idea to name it `ppp` or something else that makes sense and tells you what it does.

> **TIP**
> 
> If you have dial-on-demand enabled and your Internet connection seems to be starting periodically for no reason, a program is probably trying to do a DNS lookup. More often than not, Sendmail is the program causing problems. You can fix this by enabling the `SMART_HOST` relay definition or the `rondns` feature in the `freebsd.nc` configuration file, or by adding the IP address and hostname of your ISP’s mail server to your `/etc/hosts` file. See Chapter 24, “Configuring E-mail Services,” for information on how to configure Sendmail using the Master Config file.

> **TIP**
> 
> If you have dial-on-demand enabled and you are running Fetchmail in daemon mode so that it periodically polls your mail server, this might keep the connection open all the time in addition to causing `pppd` to dial on a regular basis. See the “E-mail for Standalone Workstations” section in Chapter 24 for ways to stop this from happening.

## Persistent Connections

You can also tell `pppd` to always keep the connection up. This is done by adding the `persist` statement to `/etc/ppp/options`. If this statement is present, `pppd` automatically tells the modem to re-establish the connection if it is lost.

> **CAUTION**
> 
> Even if your ISP tells you that you have unlimited access, make sure you read the fine print. There might be a “within reason” clause or something. If you are using the `persist` option to keep your Internet connection open 24 hours a day, 365 days a year, your ISP may terminate your account or ask you to purchase a dedicated line. The moral of this is that unlimited access does not always truly mean “unlimited access.”

## Running Commands on Connect and Disconnect

When `pppd` establishes a connection, it checks for the existence of a file called `ip-up` in `/etc/ppp`. Likewise, when the PPP connection goes down, `pppd` checks for the existence of a file called `ip-down` in `/etc/ppp`. If these files exist, whatever commands are listed in them are executed.

![](img/48eec858cce7dfb89da36a4d40b7daf3_566_0.png)

Running commands on connect or disconnect can be helpful if, for example, you are running FreeBSD on your laptop while traveling. You could read and respond to e-mail while on a plane. Then when you get to your destination and dial in to your network, you could have `pppd` flush the mail queue (deliver all the mail you wrote on the plane), as well as running the `fetchmail` program to download any new mail you had received. If you put the command to perform these options in `/etc/ppp/ip-up`, they will automatically be performed when you type **pppd** to start your dial-up connection. You could then have the `ip-down` script automatically kill `Fetchmail` if it is running in daemon mode so that it does not attempt to retrieve mail when the connection is not available.

A sample `ip-up` script could contain the following:

```
fetchmail mail.myisp.com
apache2ctl start
cd /etc/mail; make start
```

Similarly, `ip-down` could contain the following lines:

```
apache2ctl stop
cd /etc/mail; make stop
```

## Configuring User PPP

Under some circumstances, kernel PPP might not be available to you. You might, for instance, not be the administrator of the FreeBSD machine in question; or the kernel might have been compiled without PPP support. If, for whatever reason, you can't or don't want to use kernel PPP, FreeBSD also provides user PPP. User PPP does not run as a daemon and does not require PPP support to be compiled into the kernel. It does, however, require a tunnel device (`/dev/tun#`) to be compiled into the kernel; user PPP is run through a “tunnel,” meaning that the system creates a generic “virtual network interface” through which to send traffic. This interface is responsible for communicating with the PPP server, and FreeBSD does not have to do its own PPP encapsulation.

> **NOTE**
> 
> Tunnels are a mechanism frequently used in cases where an application must “fool” the operating system into supporting a certain kind of specialized traffic. Other cases where tunneling is used include compressed data streams and Virtual Private Networks (VPNs), in which each packet is encrypted. Because most operating systems don't support these protocols natively in their TCP/IP stacks, a generic tunnel is used to set up a normal TCP/IP connection, and the tunnel handlers on both sides handle decrypting or uncompressing the traffic as necessary. User PPP in FreeBSD operates in much the same way.

The first thing to do when setting up user PPP is to make sure a tunnel device is available (there should be unless you have built a custom kernel and removed it). If you have built a custom kernel, check your kernel configuration file in `/sys/i386/conf` for the line `pseudo-device tun`. If this line exists, your kernel is configured to use a tunnel device.

### The /etc/ppp/ppp.conf File

The `/etc/ppp/ppp.conf` file is the configuration file for user PPP. A sample configuration file is present in `/etc/ppp` that you can use to get started; it's set up to use CHAP or PAP authentication. You have to change several lines in it, however, to make it work with your ISP. Listing 23.1 shows the sample configuration file included with FreeBSD, along with explanations of the items you may have to change. You must be root to edit this file.

```
LISTING 23.1    Sample User PPP Configuration

# PPP  Sample Configuration File
# Originally written by Toshiharu OHNO
# Simplified 5/14/1999 by wself@cdrom.com
#
# See /usr/share/examples/ppp/ for some examples
#
# $FreeBSD: src/etc/ppp/ppp.conf,v  1.8  2001/06/21 15:42:26 brian Exp
#

default:
set log Phase Chat LCP IPCP CCP tun command
ident user-ppp VERSION (built COMPILATIONDATE)

# Ensure that "device" references the correct serial port
# for your modem. (cuaa0 = COM1, cua1 = COM2)
#
set device /dev/cuaa1

set speed 115200
set dial "ABORT BUSY ABORT NO\sCARRIER TIMEOUT 5 \\
        \"\" AT OK-AT-OK ATE1QO OK \\DATDT\T TIMEOUT 40 CONNECT"
set timeout 180                                # 3 minute idle timer (the default)
enable dns                                     # request DNS info (for resolv.conf)

papchap:
#  #
# edit the next three lines and replace the items in caps with
# the values which have been assigned by your ISP.
#
set phone PHONE_NUM
set authname USERNAME
set authkey PASSWORD
set ifaddr 10.0.0.1/0 10.0.0.2/0 255.255.255.0 0.0.0.0
add default HISADDR  # Add a (sticky) default route
```

Here is what the various options mean:

- **set device**—This option should point to the device name that your modem is on. Here is a list of the DOS equivalents: COM1: `/dev/cuaa0`, COM2: `/dev/cuaa1`, COM3: `/dev/cuaa2`, COM4: `/dev/cuaa3`.
- **set log**—This option controls what types of events get logged, and it can be useful for debugging connection problems. This option will be covered more in the section on troubleshooting.
- **set speed**—This option sets the speed at which the serial port should run. The default setting of **115200** will work for most people. If you have problems with this on an older system, you may want to change it to **57600**.
- **set dial**—This option is the modem control string for the dialer. It is similar to the chat script used for kernel PPP. The default script will work for most people, so don't change this setting unless you have problems or are familiar with your modem's command set.
- **set ifaddr**—The part of the first number (**10.0.0.1/0**) that precedes the slash should be replaced with the IP address assigned to you by your ISP. If you have a dynamic IP address, leave the number as-is. The second number (**10.0.0.2/0**) should be replaced by the gateway address your ISP gave you. If your ISP has not given you a gateway address, leave this number as-is. The third number (**255.255.255.0**) is the netmask. Unless your ISP has given you a netmask number that differs from this number, you should leave this number as-is. For instance, a customized **ifaddr** line might look like this:

```
set ifaddr 64.41.131.102/0 64.41.131.1/0 255.255.255.0 0.0.0.0
```

- **set timeout**—The number here is the number of seconds of inactivity (no outgoing or incoming traffic) that will pass before the connection is terminated. It is similar to the **idle** option in kernel PPP.
- **set default HISADDR**—This line adds a default route to the routing tables for your ISP's gateway. Note that this line must appear after the **set ifaddr** line; otherwise, PPP will not know what the gateway address is.

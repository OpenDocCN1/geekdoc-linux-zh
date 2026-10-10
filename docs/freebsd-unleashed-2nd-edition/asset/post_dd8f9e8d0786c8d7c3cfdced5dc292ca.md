
## NOTE

As long as you're on the same LAN as the FreeBSD machine, you can modify the routes—including the default route—without losing network connectivity. If you're going through these examples while connected via Telnet or SSH, you may have accidentally disconnected yourself with the `ifconfig` examples. This won't happen if you're just setting the router address, as long as there aren't any routers between you and the FreeBSD machine.

The first thing to do is to check the output of `netstat -rn`. The `netstat` tool displays the state of the routing tables and other network information; the `-r` option tells it to show the currently configured routes, and `-n` says to show the addresses numerically (rather than trying to resolve them into hostnames). This will show what default route is currently set, if any:

```
# netstat -rn
Routing tables

Internet:
Destination     Gateway         Flags     Refs     Use  Netif Expire
default      64.41.131.1     UGSc        1       1    fxp0
...
```

It seems you already have a gateway router set. This will almost certainly be the case whether the network is running properly or not; there is little error-checking in `route`, and it's pretty easy to set up a default route that would be unreachable from any of your LANs. The system might also set up a dummy default route. In any case, setting a new router address is a two-step process: You must first delete the existing default route and then you must add the new one:

```
# route delete default
delete net default
# route add default 64.2.43.1
add net default: gateway 64.2.43.1
```

## NOTE

It's worth pointing out that the `route` command is one of those parts of Unix that gives people fits because it's implemented differently on almost every single Unix variant on the planet. The differences are subtle and syntactical; although the functionality is pretty much the same, whether you're on FreeBSD or Linux or Solaris or IRIX, the way you access that functionality is maddeningly varied. To get an idea of this lack of standardization, install portentry (from `/usr/ports/security`), and look through `/usr/local/etc/portentry.conf`. It lists no fewer than nine different ways (on nine different platforms) to use `route` to set up a "blackhole" route. It's a bit ridiculous, but that's part of the price we pay for the flexibility we demand from Unix.

### Using hostname

Setting your machine’s hostname is dead simple. All it involves is the `hostname` command, with the desired hostname (as a fully qualified domain name) as its argument:

```
# hostname tiger.somewhere.com
```

You can also print out the currently set hostname in either fully qualified or standalone format:

```
# hostname
tiger.somewhere.com
# hostname -s
tiger
```

### Network Settings in /etc/rc.conf

Now that you have command-line tools at your disposal for setting the IP address, netmask, hostname, and gateway router, and now that you’ve seen how to set them manually on a one-time basis, it’s time to make sure the system takes care of all that for us. That’s what `/etc/rc.conf` is for, as you’ll no doubt recall from Chapter 10, “System Configuration and Startup Scripts.”

Recall that the system’s default settings are in `/etc/defaults/rc.conf` (which shouldn’t be touched), and any overrides that supersede those defaults go into `/etc/rc.conf`. If you look in the defaults file, you’ll find vague, generic, disabled settings for the various TCP/IP options. You’ll be enabling your Ethernet cards permanently by putting everything relevant into `/etc/rc.conf`. If you’ve configured the card using `sysinstall` (as we discussed earlier in the chapter), there will already be some settings in the file, such as the following (a block of “deltas” is added each time you use `sysinstall` to change the configuration):

```
# -- sysinstall generated deltas -- #
ifconfig_fxp0="inet 64.41.131.102  netmask 255.255.255.0"
network_interfaces="fxp0 fxp1 lo0"
defaultrouter="64.41.131.1"
hostname="tiger.somewhere.com"
```

> **TIP**
> The order in which these options are specified doesn’t matter; the startup scripts read them all into variables at once.

The values written into the file by `sysinstall` include the following:

- `network_interfaces`, which sets an explicit list of the interfaces on your system
- An `ifconfig_xxx#` line for each interface, which is precisely what is passed to `ifconfig` by the configuration scripts for each card specified in `network_interfaces`
- `defaultrouter`, which sets just what you think it does
- `hostname`, which is the fully qualified domain name

All these values are read into the resource-configuration scripts when the system boots and are passed to the appropriate utilities (`ifconfig`, `route`, and `hostname`) automatically.

Perhaps you’re wondering, What about DNS? We’ll be getting to that shortly. DNS isn’t really a part of the TCP/IP stack configuration; it’s an application-level helper service, consulted independently by networking applications before any connections are really initiated, and we don’t need it in place to get networking up and running.

### Using /etc/netstart

A nice courtesy provided by FreeBSD is the `/etc/netstart` script. It’s not a necessary part of the boot-time configuration process, and it can safely be removed from your system without hurting anything (although that would be silly, considering how useful it is). At one time, most network services were started explicitly within `/etc/netstart`. Back in the days when administrators had to edit scripts to add new services, it was a crucial part of the resource-configuration process. Now, though, in keeping with FreeBSD’s ideal of pushing all user-level and system-level script functions apart from each other, we have `/etc/rc.network`. This system-level script runs at boot time in a cascade with the rest of the resource-configuration scripts. We also have `/etc/netstart`, a user-level script that can be run at any time.

The function of `/etc/netstart` is to read in any new configuration changes from `/etc/rc.conf` and start up the network—restarting it, effectively. If you take a quick look through the script, you’ll see that there’s not a lot to it. It reads in `/etc/defaults/rc.conf`, applies the overrides from `/etc/rc.conf`, and then runs `/etc/rc.pccard` and `/etc/rc.network` in sequence. Everything in `/etc/defaults/rc.conf` and `/etc/rc.conf` is available to `rc.network` when it’s run at boot time, but not if you were to run it separately on your own. That’s what `/etc/netstart` is for; it’s a wrapper for `rc.network` that makes it behave as if the machine were just now booting.

> **NOTE**
> At the time of this writing, FreeBSD is in the process of transitioning to a new layout for the Resource Configuration files, which you learned about in Chapter 10. Later versions of the operating system may call scripts in `/etc/rc.d`, instead of the corresponding `/etc/rc.*` scripts that appeared in earlier versions.

The various command-line tools that we've just discussed—ifconfig, route, hostname, and the like—are all run from within `/etc/rc.network`, subject to various conditionals and consistency checks, and with syntax built up from the various settings to prevent input errors and potential illegal maneuvers. For everyday networking changes, `/etc/netstart` is the best and safest way to activate networking configuration changes, rather than running the various commands individually.

There's a caveat, however. The `/etc/netstart` script sets the default gateway using the route command, as you've seen; however, you can't add a new default route without deleting the old one first. The `/etc/rc.network` script doesn't issue a `route delete` default command—because it's designed to run at boot time, it shouldn't need to. So to use `/etc/netstart`, you have to delete the default route first. This makes using `/etc/netstart` a two-step process, as shown in Listing 22.1.

## LISTING 22.1   Restarting the Network Using /etc/netstart

```
# route delete default
delete net default
# /etc/netstart
Doing stage one network startup:
Doing initial network setup:.
fxp0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
        inet6 fe80::2d0:bfff:fec7:74f1%fxp0 prefixlen 64 scopeid 0x1
        inet 64.41.131.101 netmask 0xffffff00 broadcast 64.41.131.255
        ether 00:d0:b7:c7:74:f1
        media: autoselect (100baseTX <full-duplex>) status: active
        supported media: autoselect 100baseTX <full-duplex> 100baseTX
        10baseT/UTP <full-duplex> 10baseT/UTP
lo0: flags=8849<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
        inet6 fe80::1%lo0 prefixlen 64 scopeid 0x9
        inet6 ::1 prefixlen 128
        inet 127.0.0.1 netmask 0xff000000
add net default: gateway 64.41.131.1
Additional routing options: tcp extensions=NO TCP keepalive=YES.
Routing daemons:.
```

This will work fine if you're on the same LAN as the FreeBSD machine or logged in at the console. You may have noticed, however, that this will contain a nasty trap if you're controlling the machine from elsewhere in the Internet. When you delete the default route, you effectively make the machine unable to communicate with you further, so you can't issue the `/etc/netstart` command (which re-enables the default route).

A trick to get around this is to put both commands on the same line, separated using a semicolon (;). This is risky because it still has the potential to result in a few dropped

# THE SERVER

When all computers on the network are set up with their proper addressing, it is time to set up the IP masquerading rules on rumble. First, you’ll need to load the appropriate modules before you can set up any rules:

```
modprobe ip_tables
modprobe ip_conntrack
modprobe ip_conntrack_ftp
```

These modules are a minimum; you might need (or want) more. Add the module names to `/etc/modules/default` (as discussed in Chapter 19, “Kernel Modules”) so they’ll load during system boot. Other modules you might want are discussed in Chapter 35, “IP Masquerading,” and Chapter 36, “IP Firewalling.”

Now for the basic rules. The sample rules in Chapter 35 are similar to what you’ll see here, but more detailed.

The following line must be placed in rumble’s `/etc/rc.d/rc.local` file or another file that you call from `rc.local` (something like `rc.iptables` would be good):

```
iptables -t nat -A POSTROUTING -o ppp0 -s 192.168.1.0/24 -j MASQUERADE
```

If you are not connected through an analog modem, but perhaps have a permanent connection to the Internet (using cable modem or DSL) with a permanent IP (here assuming your ISP assigned you `209.127.112.160`), you’ll want to substitute the following line for the previous one:

```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to 209.127.112.160
```

At this point, you should be able to pass packets from any host that uses rumble as a gateway. If you made changes to `/etc/rc.d/rc.local` and `/etc/modules/default`, this will happen automatically when you reboot.

Of course, this is all for naught if there is no Internet connection on rumble, so a reliable dial-up connection to an Internet provider is required. For this network, a simple PAP authenticated PPP connection (by far the most common method used today with most ISPs) is assumed. Following the instructions listed in Chapter 24, “Connecting to an ISP,” a pap-secrets file and an options file are created in the `/etc/ppp` directory. For this example, the following is assumed for the dial-up Internet account:

```
Username: myname
Password: mypass
ISP phone number: 555-1111
Address is allocated: dynamically
Modem port: /dev/ttyS1 (the same as COM2 under DOS/Windows)
```

With these assumptions, the pap-secrets and options file looks like that shown in Listing 30.4.

```
LISTING 30.4    /etc/ppp/pap-secrets

# Secrets for authenticating using PAP
# client        server        secret        IP addresses
myname         *             mypass
```
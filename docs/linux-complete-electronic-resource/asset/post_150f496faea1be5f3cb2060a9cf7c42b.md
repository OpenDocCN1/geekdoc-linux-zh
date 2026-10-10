
# Handling E-mail

The previous section shows how to handle the outgoing mail—simply by flushing the mail queue once the link is up.

If you are running a WAN link, you can arrange with the network administrator of the remote LAN to do exactly the same thing. For example, at the Newman Campus end of our WAN link, the /etc/ppp/ip-up script looks like:

```bash
#!/bin/bash

# Script which handles the routing issues as necessary for
# pppd Only the link to Hedland requires this handling.

# When the ppp link comes up, this script is called with the
# following parameters
#  $1  the interface name used by pppd (e.g. ppp3)
#  $2  the tty device name
#  $3  the tty device speed
#  $4  the local IP address for the interface
#  $5  the remote IP address
#  $6  the parameter specified by the 'iparam' option to pppd
case "$5" in
  203.18.8.4)
  /usr/sbin/sendmail -q
  ;;
  *)
esac
exit 0
```

If, however, you have only a dynamic IP PPP link to your ISP, you need to get your e-mail from the account on your ISP’s machine. This is usually done using the POP (Post Office Protocol). This process can be handled using the popclient program—and the ip-up script can automate this process for you too.

Simply create a /etc/ppp/ip-up script that contains the appropriate invocation of popclient. For my laptop that runs Red Hat Linux (which I take on any travels), this is:

```bash
popclient -3 -c -u hartr -p <password> kepler.hedland.edu.au | formail -s proclaim
```

You could use slurp or whatever to do the same for news, and so forth. Remember, the ip-up script is just a standard bash script and so can be used to automate *any* function that needs to be accomplished every time the appropriate PPP link comes up.

## USING /ETC/PPP/IP-DOWN

You can create a script that will be executed once the link has been terminated. This is stored in `/etc/ppp/ip-down`. It can be used to undo anything special that you did in the corresponding `/etc/ppp/ip-up` script.

## ROUTING ISSUES ON A LAN

If you are connected to a LAN but still want to use PPP on your personal Linux machine, you need to address some issues of the routes packets need to take from your machine to reach your LAN (through your Ethernet interface) and also to the remote PPP server and beyond.

This section does *not* attempt to teach you about routing—it deals only with a simple, special case of (static) routing.

I strongly urge you to read the Linux Network Administrator Guide (NAG) if you are *not* familiar with routing. Also the O’Reilly book *TCP/IP Network Administration* covers this topic in a very understandable form.

The basic rule of static routing is that the *default* route should be the one that points to the *most* number of network addresses. For other networks, enter specific routes to the routing table.

The *only* situation I am going to cover here is where your Linux box is on a LAN that is not connected to the Internet—and you want to dial out to the Internet for personal use while still connected to the LAN.

First of all, make sure that your Ethernet route is set up to the specific network addresses available across your LAN—*not* set to the default route. Check this by issuing a route command; you should see something like the following:

```text
[root@win /root]# route -n
Kernel routing table
Destination     Gateway     Genmask     Flags MSS Window Use Iface
loopback        *         255.255.255.0 U   1936    0     50  lo
10.0.0.0        *         255.255.255.0 U   1436    0     565 eeth0
```

If your Ethernet interface (eth0) is pointing at the default route (the first column will show *default* in the eth0 line) you need to change your Ethernet initialization scripts to make it point at the specific network numbers rather than the default route (consult the Net2 HOWTO and NAG).

This will allow pppd to set up your default route as shown below:

```text
[root@hw1n /root]# route -n
Kernel routing table

Destination     Gateway     Genmask     Flags MSS Window Use Iface
10.144.153.51   *         255.255.255.255 UH 488 0      0   ppp0
127.0.0.0       *         255.255.255.0 U    1936 0      50  lo
10.1.0.0        *         255.255.255.0 U    1436 0      569 eth0
default         10.144.153.51               UG 488 0      3   ppp0
```

As you can see, we have a host route to the PPP server (10.144.153.51) via ppp0 and also a default network route that uses the PPP server as its gateway.

If your setup needs to be more complex than this, read the routing documents already mentioned and consult an expert at the site.

If your LAN already has routers on it, you will already have gateways established to the wider networks available at your site. You should still point your default route at the PPP interface—and make the other routes specific to the networks they serve.

## Note on Security

When you set up a Linux box on an existing LAN to link into the Internet, you are potentially opening your entire LAN to the Internet—and the hackers that reside there. Before you do this, I strongly urge you to consult your network administrator and site security policy. If your PPP connection to the Internet is used to successfully attack your site, you will at the very least earn the intense anger of your fellow users and network and system administrators. You may also find yourself in much more serious trouble!

Before you connect a LAN to the Internet, you should consider the security implications of even a dynamic connection—hence the earlier reference to the O’Reilly *Building Internet Firewalls*.

## SETTING UP A PPP SERVER

As already mentioned, there are many ways to do this. What I present here is the way I do it (using a Cyclades multiport serial card) and a rotary dial-in set of telephone lines.

![](img/a3584dae761d2e3abed8bf40d7637389_380_0.png)

If you don’t like the method I present here, please feel free to go your own way. I would, however, be pleased to include additional methods in future versions of the HOWTO. So, please send me your comments and methods.

Please note, this section only concerns setting up Linux as a PPP server. I do not (ever) intend to include information on setting up special terminal servers and such.

Also, I have yet to experiment with shadow passwords (but will be doing so sometime). Information currently presented does not therefore include any bells and whistles that are required by the shadow suite.

## Kernel Compilation

All the earlier comments regarding kernel compilation and kernel versions versus pppd versions apply. This section assumes that you have read the earlier sections of this document!

For a PPP server, you *must* include IP forwarding in your kernel. You may also wish to include other capabilities (such as IP firewalls, accounting, etc.).

If you are using a multiport serial card, then you must obviously include the necessary drivers in your kernel too.

## Overview of the Server System

We offer dial-up PPP (and SLIP) accounts and shell accounts using the same user name/password pair. This has the advantages (for us) that a user requires only one account and can use it for all types of connectivity.

As we are an educational organization, we do not charge our staff and students for access, and so do not have to worry about accounting and charging issues.

We operate a firewall between our site and the Internet, and this restricts some user access as the dial-up lines are inside our (Internet) firewall (for fairly obvious reasons, details of our other internal firewalls are not presented here and are irrelevant in any case).

The process a user goes through to establish a PPP link to our site (once they have a valid account of course) is:

- Dial into our rotary dialer (this is a single phone number that connects to a bank of modems—the first free modem is then used).
- Log in using a valid user name and password pair.
- At the shell prompt, issue the command ppp to start PPP on the server.
- Start PPP on their PC (be it running Windows, DOS, Linux, Mac OS or whatever—that is their problem).

The server uses individual /etc/ppp/options.ttyXX files for each dial-in port that sets the remote IP number for dynamic IP allocation.

The server users proxyarp routing for the remote clients (set via the appropriate option to pppd). This obviates the need for routed or gated.

When the user hangs up at their end, pppd detects this and tells the modem to hang up, bringing down the PPP link at the same time.

## Getting the Software Together

You will need the following software:

- Linux, properly compiled to include the necessary options.
- The appropriate version of pppd for your kernel.
- A getty program that intelligently handles modem communication. We use gettys2.0.7h, but mgetty is highly thought of. I understand that mgetty can detect a call that is using PAP/CHAP (PAP is the standard for Windows 95) and invoke pppd automatically, but I have yet to explore this.
- An operational domain name server (DNS) that is accessible to your dial-up users. You should really be running your own DNS if possible...

## Setting up Standard (Shell Access) Dialup

Before you can set up your PPP server, your Linux box must be capable of handling standard dial-up access.

This howto does not cover setting this up. Please see the documentation of the getty of your choice and serial HOWTO for information on this.

This line differs from the one presented earlier only in the absence of the -r parameter.
The mgetty program was designed for use with modems (hence the m in mgetty), so the
-r parameter disables some normal mgetty functionality. Specifically, mgetty normally
sends command codes to the modem to prepare it to receive calls, and mgetty responds
to a modem's connect messages by passing it the login prompt. Removing the
-r parameter from the /etc/inittab line re-enables these features.

# Administrator's Logbook: Accepting Remote Logins

System: E123456728

Action: Configured system to accept remote logins via /dev/ttyS1, with 57,600 bps
port speed and mgetty.

File modified: /etc/inittab

# Accepting PPP Connections

It's desirable to configure a Linux system to accept PPP logins. So configured,
an an Internet-enabled Linux computer can function as a gateway between a remote com-\puter running any of several operating systems and the Internet. This setup can be con-
ven if you have a system at work with always-on Internet access and a modem, and
you want to provide yourself or your employees with Internet access at home or when
they are on the road. Many ISPs use Linux systems running PPP servers to handle doz-
ends, hundreds, or more users.

> NOTE 56Kbps modems operate with a speed asymmetry—upload speeds are
lower than download speeds. This state of affairs exists because the high
upload speeds require that one (the ISP's) computer in a normal configur-
ration) have a special connection to the telephone network. Unless you acquire
such a connection, your dial-in PPP system will be limited to 33.6Kbps speeds,
even if you have a 56Kbps modem.

There are many ways to accept PPP connections. The method described here is compar-
tively simple to set up, but it requires that the calling system use a connection script or
ually enter authentication information. No matter how you do it, there are several
configuration features you must set. In essence, a PPP link requires that the Linux-
puter function as a router between the dial-in systems and the rest of the network. There-
fore, these systems require router support in the Linux kernel (which is standard in most
Linux distributions, including Red Hat 7.0). You must also be able to assign an IP address
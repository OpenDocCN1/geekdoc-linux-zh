This line differs from the one presented earlier only in the absence of the -r parameter. The mgetty program was designed for use with modems (hence the m in mgetty), so the -r parameter *disables* some normal mgetty functionality. Specifically, mgetty normally sends command codes to the modem to prepare it to receive calls, and mgetty responds to a modem's connect messages by running the Linux login program on the serial port. Removing the -r parameter from the /etc/inittab line re--enables the use of modem configuration commands.

# Administrator's Logbook: Accepting Remote Logins

System: E12345678

Action: Configured system to accept remote logins via /dev/ttyS1, using 57,600bps port speed and mgetty.

File modified: /etc/inittab

# ## Accepting PPP Connections

It's sometimes desirable to configure a Linux system to accept PPP logins. So configured, an Internet--enabled Linux computer can function as a gateway between a remote computer running any of several operating systems and the Internet. This setup can be convenient if you have a system at work with always--on Internet access and a modem, and you want to provide yourself or your employees with Internet access at home or when you or they are on the road. Many ISPs use Linux systems running PPP servers to handle dozens, hundreds, or more users.

**Note** 56Kbps modems operate with a speed asymmetry--upload speeds are slower than are download speeds. This state of affairs exists because the high upload speeds require that one system (the ISP's computer in a normal configuration) have a special connection to the telephone network. Unless you acquire such a connection, your dial--in PPP system will be limited to 33.6Kbps speeds, even if both sides use 56Kbps modems.

There are many ways to accept PPP connections. The method described here is comparatively simple to set up, but it requires that the calling system use a connection script or manually enter authentication information. No matter how you do it, there are several configuration features you must set. In essence, a PPP link requires that the Linux computer function as a router between the dial--in systems and the rest of the network. Therefore, these systems require router support in the Linux kernel (which is standard in most Linux distributions, including Red Hat 7.3). You must also be able to assign an IP address to the dial--in systems. Normally, this is done on a static basis according to the serial port, as you'll shortly see.

To configure a Linux system as a PPP server, follow these steps:

+   1.  Configure the computer to accept a remote login via a getty program, as described in the previous section.
2.  Modify the /etc/ppp/options file so that it contains the following entries (you may need to modify the netmask to conform to your network; this value should be the same as the netmask of the PPP server):

```
asyncmap 0
netmask 255.255.255.0
proxyarp
```
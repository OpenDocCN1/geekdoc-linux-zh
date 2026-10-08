# 510 CONNECTING TO THE INTERNET

Before you begin to use PPP, you must at least configure the loopback device. Furthermore, you must compile the appropriate driver for PPP into the kernel or load it as a module. Modules can be loaded into memory on demand by means of the kerneld daemon; they are removed when they are no longer needed. By means of the dialad daemon, you can automatically dial your provider as soon as a program needs to use a network service.

This chapter can only give a simple introduction to a complex subject. You should in any case consult the man pages and HowTo documents of the LDP project, with the indicated RFCs, which may also be helpful.

# 23.1 Point-to-Point Protocol (PPP)

The Point-to-Point Protocol (PPP), described in [rfc1661], is based on the experience gained with implementation and application of SLIP (Serial Line Internet Protocol; now obsolete). Today, every provider supports PPP, so you should use this protocol. In addition, PPP can be used to transmit other protocols besides IP, such as IPX or AppleTalk. Further information on PPP can be found in the PPP HowTo of the Linux Documentation Project and in the main page for pppd.

For using PPP, you will need the appropriate kernel support (compiled into the kernel or as a module). In addition, the pppd daemon that suits your kernel version must be installed on your system.

# 23.1.1 Dial-up IP with PPP

If the connection to the PPP server is already established and the PPP driver is loaded on the server, the PPP link is opened with the following command:

```
(Linux):~# pppd /dev/ttyS1 38400 crts defaultroute
```

The serial interface tty1 is put into PPP mode, and the speed is set to 38 400 bps, using hardware handshake. This link is installed as the default route; this is one of the reasons pppd must be started by root. If non-privileged users are also allowed to be open a PPP link, you must start the setuid program (chmod 1). You can restrict execution rights to a group of users, see also Section 4.4. Otherwise you may use sudo.

Before payload data can be transmitted via this connection, you must specify the connection parameters, such as the IP address and MTU. If you have not specified any special settings, these are negotiated with the server with the aid of the IP Control Protocol (IPCP), which is a dialogue between computers

![](bbox=[0.15, 0.935, 0.235, 0.955])
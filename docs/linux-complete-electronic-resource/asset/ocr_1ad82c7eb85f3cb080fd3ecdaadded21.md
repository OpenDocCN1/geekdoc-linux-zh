# Maintaining a Permanent Connection to the Net with *pppd*

If you are fortunate enough to have a semi-permanent connection to the Net and would like to have your machine automatically read your PPP connection if it is lost, then here is a simple trick to do so.

Configure PPP such that it can be started by the *root* user by issuing the command:

```
# pppd
```

*Be sure* that you have the “-detach” option configured in your */etc/ppp/options* file. Then insert the following line into your */etc/inittab* file, down with the *getty* definitions:

```
pd:23:respawn:/usr/sbin/pppd
```

This will cause the *init* program to spawn and monitor the *pppd* program and automatically restart it if it dies.

# slip Client

*slip* devices are named “*s10*”, “*s11*”, etc. with the first device configured being assigned “*0*” and the rest incrementing sequentially as they are configured.

**Kernel Compile Options:**

```
Network device support --->
[*] Network device support
<*> SLIP (serial line) support
[ ] CSLIP compressed headers
[ ] Keepalive and linefill
[ ] Six bit SLIP encapsulation
```

*slip* (Serial Line Internet Protocol) allows you to use TCP/IP over a serial line, be that a phone line with a dial-up modem, or a leased line of some sort. Of course to use *slip* you need access to a *slip-server* in your area. Many universities and businesses provide *slip* access all over the world.

*slip* uses the serial ports on your machine to carry IP datagrams. To do this it must take control of the serial device. *slip* device names are named *sl0*, *sl1*, etc. How do these correspond to your serial devices? The net-working code uses what is called an *ioctl* (i/o control) call to change the serial devices into *slip* devices. There are two programs supplied that can do this: *dip* and *sattach*
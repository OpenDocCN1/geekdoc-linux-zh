After configuration has finished, use the ads1-start command to start a connection and DSL session, like this:

```
$ sudo /sbin/ads1-start
```

The DSL connection should be nearly instantaneous, but if problems occur, check to make sure that your DSL modem is communicating with the phone company's central office by examining the status LEDs on the modem. Because this varies from modem to modem, consult your modem user's manual.

Check to make certain that all cables are properly attached, that your interfaces are properly configured, and that you have entered the correct information to the setup script.

If IP masquerading is enabled, other computers on your LAN on the same subnet address (such as 192.168.1.XXX) can use the Internet, but must have the same /etc/resolv.conf name server entries and a routing entry with the DSL-connected computer as a gateway. For example, if the host computer with the DSL connection has an IP address of 192.168.1.1, and other computers on your LAN use addresses in the 192.168.1.XXX range, use the route command on each computer like this:

```
# /sbin/route add default gw 192.168.1.1
```

Note that you can also use a hostname instead if each computer has an /etc/hosts file with hostname and IP address entries for your LAN. To stop your connection, use the ads1-stop command like this:

```
# /sbin/ads1-stop
```

# Configuring Dial-Up Internet Access

Most ISPs provide dial-up connections supporting PPP because it is a fast and efficient protocol for using TCP/IP over serial lines. PPP is designed for two-way networking; TCP/IP provides the transport protocol for data. One hurdle faced by new Ubuntu users is how to set up PPP and connect to the Internet. It is not necessary to understand the details of the PPP protocol in order to use it, and setting up a PPP connection is easy. You can configure the PPP connections manually using the command line or graphically during an X session using Ubuntu's Internet Configuration Wizard. Each approach produces the same results.

PPP uses several components on your system. The first is a daemon called pppd, which controls the use of PPP. The second is a driver called the high-level data link control (HDLC), which controls the flow of information between two machines. A third component of PPP is a routine called chat that dials the other end of the connection for you when you want it to. Although PPP has many “tunable” parameters, the default settings work well for most people.
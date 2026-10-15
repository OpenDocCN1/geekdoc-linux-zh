
protocol issues earlier on in this chapter. Advanced configuration of a firewall or router, other than what was addressed during your initial installation of Ubuntu, is beyond the scope of this book.

## Understanding Point-to-Point Protocol over Ethernet

Establishing a DSL connection with an ISP providing a static IP address is easy. Unfortunately, many DSL providers use a type of PPP protocol named Point-to-Point Protocol over Ethernet (PPPoE) that provides dynamic IP address assignment and authentication by encapsulating PPP information inside Ethernet frames. Roaring Penguin’s rp-pppoe clients are available from the Roaring Penguin site (www.roaringpenguin.com/penguin/pppoe/rp-pppoe-3.8.tar.gz), and these clients make the difficult-to-configure PPPoE connection much easier to deal with. You can download and install newer versions (see the Roaring Penguin link in the “Reference” section at the end of this chapter).

> **NOTE**
>
> ADSL modems were frequently supplied by ISPs when they originally started to roll out ADSL services. Nowadays, however, these modems are optional, which is a good thing as many people choose to purchase a router with an in-built modem to create a dedicated connection. Using a router can save many headaches and will allow you to easily connect more than one computer to an Internet connection. Note that if you are using a cable connection, then they usually come with an Ethernet cable, in which case you just need a router. Check with your ISP before buying to ensure that whatever router you do end up with can be supported by them. You might find that your ISP even supplies a router as part of the package!

## Configuring a PPPoE Connection Manually

You should only need to use these steps if you are using a modem supplied by your ISP, and not a router. The basic steps involved in manually setting up a DSL connection using Ubuntu involve connecting the proper hardware, and then running a simple configuration script if you use rp-pppoe from Roaring Penguin.

First, connect your DSL modem to your telephone line, and then plug in your Ethernet cable from the modem to your computer’s network interface card. If you plan to share your DSL connection with the rest of your LAN, you need at least two network cards—designated eth0 (for your LAN) and eth1 (for the DSL connection).

The following example assumes that you have more than one computer and will share your DSL connection on a LAN.

Note that you can also use a hostname instead, if each computer has an /etc/hosts file with hostname and IP address entries for your LAN. To stop your connection, use the adsl-stop command like this:

```
# /sbin/adsl-stop
```

## Configuring Dial-Up Internet Access

Most ISPs provide dial-up connections supporting PPP because it is a fast and efficient protocol for using TCP/IP over serial lines. PPP is designed for two-way networking; TCP/IP provides the transport protocol for data. One hurdle faced by new Ubuntu users is how to set up PPP and connect to the Internet. It is not necessary to understand the details of the PPP protocol in order to use it, and setting up a PPP connection is easy. You can configure the PPP connections manually using the command line or graphically during an X session using Ubuntu’s Network Configuration Tool. Each approach produces the same results.

PPP uses several components on your system. The first is a daemon called pppd, which controls the use of PPP. The second is a driver called the High-Level Data Link Control (HDLC), which controls the flow of information between two machines. A third component of PPP is a routine called chat that dials the other end of the connection for you when you want it to. Although PPP has many “tunable” parameters, the default settings work well for most people.

## Configuring a Dial-Up Connection Manually

Ubuntu includes some useful utilities to get your dial-up connection up and running. In this section we will take a look at two options that will have you on the Internet in no time.

The first way is to configure a connection using `pppconfig`, a command line utility to help you to configure specific dial-up connection settings.

Enter the following command:

```
$ sudo pppconfig
```

Before you connect for the first time you need to add yourself to both the dip and dialout groups by using the commands:

```
$ sudo adduser YOURNAMEHERE dip
$ sudo adduser YOURNAMEHERE dialout
```

Once this has been done it is just a simple matter of issuing the `pon` command to connect, and the `poff` command to disconnect. You can create as many different profiles as you

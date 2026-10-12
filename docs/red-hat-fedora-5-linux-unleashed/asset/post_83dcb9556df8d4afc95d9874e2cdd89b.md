
as well as how to configure Fedora to provide dial-in PPP support. The chapter also describes how to use Roaring Penguin's DSL utilities for managing connectivity through a cable modem connection.

## Linux and America Online

The America Online service (AOL) used to be often cited as a reason that many more people don't use Linux. Why? Because AOL uses a proprietary protocol to connect and a proprietary client to access AOL content; no Linux interface is available, with no signs that AOL is about to provide one. Simply put, if you wanted to use Linux, you were forced to choose some Internet connection other than AOL.

Work was done on a client that would allow an AOL user to connect to the AOL service and at least access the Internet. The Penggy (formerly Pengaal) page at http://www.peng.apinc.org/eng/ provides links to binary RPM packages as well as source tarballs and HOWTOS. This software is not sanctioned by AOL, but it might allow an AOL user to experiment with Linux.

The situation is quite different if you are one of the many using a broadband connection to get onto AOL. Because routers tend to be OS-agnostic, you can easily connect a Linux machine to the network and access the Internet. In fact, the computer that I am typing this on is connected to AOL via a router. Okay, you will not get the AOL-specific content, but then again, are you really going to miss it?

## Common Configuration Information

Although Fedora enables great flexibility in configuring Internet connections, that flexibility comes at the price of an increase in complexity. To configure Internet connectivity in Fedora, you must know more about the details of the connection process than you can learn from the information typically provided by your Internet service provider (ISP). In this section of the chapter, you learn what to ask about and how to use the information.

Some ISPs are unaware of Linux or unwilling to support its use with their service. Fortunately, that attitude is rapidly changing, and the majority of ISPs offer services using standard protocols that are compatible with Linux, even if they (or their technical support people) aren't aware that their own ISPs are Linux-friendly. You just need to press a little for the information you require.

If you are using a dial-up modem account (referred to in Linux as PPP for the Point-to-Point Protocol it uses), your ISP will provide your computer with a static or dynamic IP (Internet Protocol) address. A dynamic IP address changes each time you dial in, whereas a static IP address remains the same. The ISP also might automatically provide your computer with the names of the Domain Name Service (DNS) servers. You need to know the telephone number that your computer will dial in to for making the connection; your ISP supplies that number, too. You will also need a working modem and need to know the device name of the modem (usually /dev/modem).

> Most IP addresses are dynamically assigned by ISPs; ISPs have a pool of addresses, and you get whatever address is available. From the ISP’s viewpoint, a small number of addresses can serve a large number of people because not everyone will be online at the same time. For most Internet services, a dynamic IP works well because it is the ISP’s job to route that information to you, and it sits in the middle—between you and the service you want to use. But a dynamic IP address changes, and if someone needs to find you at the same address (if you run a website or a file transfer site, for example), an IP that changes every time you log on will not work well. For that, you need a static IP. Because your ISP cannot reuse that IP with its other customers, it will likely charge you more for a static IP than for a dynamic IP. The average consumer doesn’t need the benefit of a static IP, so he is happily paying less for a dynamically assigned IP. Also, the DNS information can be provided automatically by the ISP by the Dynamic Host Configuration Protocol, or DHCP.

If you are using DSL access or a cable modem, you might have a dynamic IP provided through DHCP, or you might be assigned a static IP. You might automatically be provided with the names of the DNS servers if you use DHCP, or you might have to set up DNS manually (in which case, you have to know the IP addresses of the DNS servers).

In all cases, you have to know your username, your password, and for the configuration of other services, the names of the mail servers and the news server. This information can be obtained from your ISP if you specifically ask for it.

> The information in this book will help you understand and avoid many connection issues, but you might experience connection problems. Keep the telephone number of the technical help service for your ISP on hand in case you are not able to establish a connection. But be aware that few ISPs offer Linux support, and you might need to seek help from a Linux-savvy friend or a Linux user’s group if your special circumstances cannot be handled from the knowledge you gain from this book. Of course, the best place to look is on the Internet. Use Google’s Linux page (http://www.google.com/linux/), to research the problem and see if any other users have found fixes or workarounds.

## Configuring Digital Subscriber Line Access

Fedora also supports the use of a digital subscriber line service. Although it refers to the different types of DSL available as xDSL, that name includes ADSL, IDSL, SDSL, and other flavors of DSL service; they can all be configured using the Internet Connection Wizard. DSL service generally provides 128Kbps to 8.0Mbps transfer speeds and transmits data over copper telephone lines from a central office to individual subscriber sites (such as your home). Many DSL services provide asymmetric speeds with download speed greater than upload speeds.

**NOTE**

DSL service is an "always-on" type of Internet service, although you can turn off the connection under Fedora using the Network Device Control. An always-on connection exposes your computer to malicious abuse from crackers who trawl the Internet attempting to gain access to other computer systems. In addition to the capability to turn off such connections, Fedora provides a firewall to keep crackers out; you configured a simple firewall during the original installation. The firewall can also be configured from the Security Level Configuration tool found in the System Settings menu selection as Security Level.

A DSL connection requires that you have an ethernet network interface card (sometimes a USB interface that is not easily supported in Linux) in your computer or notebook. Many users also configure a gateway, firewall, or other computer with at least two network interface cards in order to share a connection with a LAN. We looked at the hardware and protocol issues earlier in this chapter. Advanced configuration of a firewall or router, other than what was addressed during your initial installation of Fedora, is beyond the scope of this book.

## Understanding Point-to-Point Protocol over Ethernet

Establishing a DSL connection with an ISP providing a static IP address is easy. Unfortunately, many DSL providers use a type of PPP protocol named Point-to-Point Protocol over Ethernet (PPPoE) that provides dynamic IP address assignment and authentication by encapsulating PPP information inside ethernet frames. Roaring Penguin's rp-pppoe clients are included with Fedora, and these clients make the difficult-to-configure PPPoE connection much easier to deal with. You can download and install newer versions (see the Roaring Penguin link in the “Reference” section at the end of this chapter).

## Configuring a PPPoE Connection Manually

The basic steps involved in manually setting up a DSL connection using Fedora Core Linux involve connecting the proper hardware, and then running a simple configuration script if you use rp-pppoe from Roaring Penguin.

First, connect your DSL modem to your telephone line, and then plug in your ethernet cable from the modem to your computer's network interface card. If you plan to share your DSL connection with the rest of your LAN, you need at least two network cards—designated eth0 (for your LAN) and eth1 (for the DSL connection).

The following example assumes that you have more than one computer and will share your DSL connection on a LAN. First, log in as root, and ensure that your first eth0 device is enabled and up (perhaps using the ifconfig command). Next, bring up the other interface, but assign a null IP address like this:

```
# /sbin/ifconfig eth0 0.0.0.0 up
```

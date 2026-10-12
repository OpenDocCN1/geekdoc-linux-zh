several names to a system using IP aliasing and have Web servers listen for any traffic to that address.

One of the common denial of service attacks used by system crackers and malcontents is to use TCP SYN cookies to tie up your machines’ resources and prevent legitimate users from utilizing them. Turning on the IP: TCP syncookie support option will help detect and defend against this type of attack. To use this option, you must also enable the /proc filesystem and sysctl support mentioned later on.

# Tip

Selecting this option in the kernel configuration does not turn on the feature, it only allows you to turn it on. This is done by issuing the following command:

```
echo 1 > /proc/sys/net/ipv4/tcp_syncookies
```

This is why you must enable support for the /proc filesystem and the sysctl support in order to use this feature.

# IPX and Appletalk

Two of the options available for Linux that make is so well suited in mixed networks are the options to support IPX and Appletalk protocols. These protocols allow Linux to participate in Netware and Apple networks using the native protocols. Linux can be configured to look like a Netware file and print server to Netware clients. By using the netatalk program, you can do the same for networks of Mac systems. Details on setting up this support can be found in Chapter 18, “Integrating with Other Network Operating Systems.”

For the enterprise network administrator, Linux includes support for the X.25 protocol, which is a mechanism for running multiple virtual circuits via a single physical line. This support does not include support for dedicated X.25 network cards, but does provide for X.25 services or ordinary modems and Ethernet networks using the 802.2 LLC or LAPB protocols.

Another option of interest to the enterprise network administrator is the WAN option, which allows you to turn your Linux system into a WAN router. You can also add encryption to your WAN, using software from the FreeS/WAN project in Toronto, which offers a free encryption layer, using 1,024-bit keys and 168-bit Triple-DES technology. This software also implements IPSEC, or Internet Protocol Security. This software is free from U.S. import restrictions because it was developed outside of the country.
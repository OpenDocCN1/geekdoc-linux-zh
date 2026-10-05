# Chapter 14

# TCP/IP Networking

laptop. Check browser compatibility too, since the voodoo involved in imple- menting browser-based VPN solutions often doesn't translate among browsers.

# 14.9 PPP: THE POINT-TO-POINT PROTOCOL

PPP is defined in RFC1331.

PPP represents an underlying communication channel as a virtual network inter-face. However, since the underlying channel need not any of the features of actual network, communication is restricted to the two hosts at the end of the link—a virtual network of two. PPP has the distinction of being used on both the slowest and the fastest IP links, for different reasons.

In its asynchronous form, PPP is best known as the protocol to provide dial-up Internet service over phone lines and serial lines. These channels are not in-herently part oriented, so the PPP device driver encodes packets into a unified data stream and adds link-level headers to separate packets.

Designed by committee, PPP is the "everything and the kitchen sink" encaps-lation protocol. In addition to specifying how the link is established, maintained, and down, PPP implements error checking, authentication, encryption, and compression. These features make it adaptable to a variety of situations.

PPP as a dial-up technology once an important topic for UNIX and Linux system administrators, but the widespread availability of broadband has made dial-up configuration largely irrelevant. At the same time, the high-end applic-ations of PPP have mostly retreated into various pieces of dedicated network hard-ware. These days, the primary use of PPP is to connect through cellular mediums.

# 14.10 BASIC NETWORK CONFIGURATION

Only a few steps are involved in adding a new machine to the existing area network, but every system does slightly differently. Systems typically provide a control panel GUI for basic network configuration, but more elaborate (auto-mated) setups may require you to edit the configuration files directly.

Before bringing a new machine on a network that is connected to the Internet, secure it (Chapter 22, Security) so that you are not inadvertently inviting attackers onto your local network.
# What Is PPPOE?

PPPoE is a way for broadband ISPs to assign IP addresses to customers' computers. In 2002, its use is restricted largely to low-end residential Digital Subscriber Line (DSL) accounts, although some business DSL accounts also use PPPoE. Cable modem ISPs generally use DHCP for IP address assignment, and high-end DSL accounts typically use static IP address assignment. PPPoE is a way to use Ethernet as a medium for PPP encapsulation, rather than the more common RS-232 serial line.

Why use PPPoE, though? After all, TCP/IP has been working directly on Ethernet for a long time, so PPPoE complicates matters by adding an extra layer to the Internet connection. The short answer is that PPPoE makes life easier for ISPs, by providing tools that help them manage IP addresses and monitor account usage. PPPoE offers few benefits to subscribers; however, you may have no choice but to use it with some ISPs.

# PPPoE Packages for FreeBSD

Two common approaches to using PPPoE with FreeBSD are

+   - **User-mode PPP** The same tool that provides user-mode PPP support over RS-232 serial ports also supports PPPoE. (This program is not the same as the kernel PPP daemon described in the earlier section, "Configuring Kernel PPP.")
+   - **Roaring Penguin** The Roaring Penguin package (http://www.roaringpenguin.com/PPPoE/) provides an alternative that originated in the Linux world, but is available through the FreeBSD ports system. Roaring Penguin has the advantage of offering a GUI interface.

The next section, "Configuring PPPoE," describes the standard FreeBSD user-mode PPP tool as applied to PPPoE.

# Configuring PPPoE

The main feature you need to adjust to get PPPoE working is the `/etc/ppp/ppp.conf` file. Listing 15-3 shows a typical `ppp.conf` file configured for PPPoE.

+   **Listing 15-3.**
+   Sample /etc/ppp/ppp.conf
+   File for Use
+   with PPPoE

```
default:
    set log Phase tun command
    set ifaddr 10.0.0.1/0 10.0.0.2/0

broadband_isp_name:
    set device PPPoE:fxp0
    set authname agb
    set authkey w8tS4nr6
```
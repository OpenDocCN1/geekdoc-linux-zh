The default network configuration relies on DHCP to obtain an IP address, DNS server, and gateway, but you can use the gear icon in the lower-right corner to alter the configuration in many ways (for example: set the MAC address, switch to a static setup, enable or disable IPv6, and add additional routes). You can create profiles to save multiple wired network configurations and easily switch between them. For wireless networks, their settings are automatically tied to their public identifier (SSID).

NetworkManager also handles connections by mobile broadband (Wireless Wide Area Network WWAN) and by modems using point-to-point protocol over ethernet (PPPoE). Last but not least, it provides integration with many types of virtual private networks (VPN) through dedicated plugins: SSH, OpenVPN, Cisco's VPN C, PPTP, Strogswan. Check out the `network-manager-*` packages; most of them are not installed by default. Note that you need the packages suffixed with `-gnome` to be able to configure them through the graphical user interface.

# 5.1.2. On the Command Line with ifupdown

Alternatively, when you prefer not to use (or don't have access to) a graphical desktop, you can configure the network with the already-installed `ifupdown` package, which includes the `ifup` and `ifdown` tools. These tools read definitions from the `/etc/network/interfaces` configuration file and are at the heart of the `/etc/init.d/networking` init script that configures the network at boot time.

Each network device managed by `ifupdown` can be deconfigured at any time with `ifdown network-device`. You can then modify `/etc/network/interfaces` and bring the network back up (with the new configuration) with `ifup network-device`.

Let's take a look at what we can put in ifupdown's configuration file. There are two main directives: `auto network-device`, which tells `ifupdown` to automatically configure the network interface once it is available, and `iface network-device inet/inet6 type` to configure a given interface. For example, a plain DHCP configuration looks like this:

```
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```
```

Note that the special configuration for the loopback device should always be present in this file. For a fixed IP address configuration, you have to provide more details such as the IP address, the network, and the IP of the gateway:
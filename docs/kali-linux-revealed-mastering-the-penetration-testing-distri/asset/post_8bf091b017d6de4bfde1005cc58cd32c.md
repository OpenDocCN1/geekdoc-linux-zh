
- The installation requirements for Kali Linux vary from a basic SSH server with no desktop, as little as 128 MB RAM (512 MB recommended) and 2 GB disk space, to the higher-end kali-linux-full meta-package, with at least 2048 MB of RAM and 20 GB of disk space. In addition, your machine must have a CPU supported by at least one of the amd64, i386, armel, armhf, or arm64 architectures.
- Kali can easily be installed as the primary operating system, alongside other operating systems through partitioning and boot loader modification, or as a virtual machine.
- To guarantee the confidentiality of your data, you can set up encrypted partitions. This will protect your data if your laptop or hard drive is lost or stolen.
- The installer can also be automated through debconf preseeding, a function that allows you to provide unattended answers to installation questions.
- A preseed file is a plain text file in which each line contains the answer to one Debconf question. A line is split across four fields separated by white space (spaces or tabs). You can preseed answers to the installer with boot parameters, with a preseed file in /initrd, with a preseed file on the boot media, or with a preseed file from the network.
- Kali Linux runs on a wide variety of ARM-based devices such as laptops, embedded computers, and developer boards. ARM installation is fairly straightforward. Download the proper image, burn it to an SD card, USB drive, or embedded multi-media controller (eMMC) module, plug it in, boot the ARM device, find your device on the network, log in, and change the SSH password and SSH host keys.
- You can debug failed installations with virtual consoles (accessible with the CTRL+Shift and function keys), debconf-get and debconf-set commands, reading the /var/log/syslog log file, or by submitting a bug report with log files retrieved with the installer's “Save debug logs” function.

Now that we have discussed Linux fundamentals and Kali Linux installation, let's discuss configuration so you can begin to tailor Kali to suit your needs.

# Keywords

- Network
- Users and groups
- Services
- Apache
- PostgreSQL
- SSH

![](img/46e3313ea1bb2892f314630a4f0677b8_128_0.png)

# Chapter 5

Configuring Kali Linux

- Configuring the Network 104
- Managing Unix Users and Unix Groups 107
- Configuring Services 109
- Managing Services 117
- Summary 119

In this chapter, we will take a look at various ways you can configure Kali Linux. First, in section 5.1, "Configuring the Network" [page 104], we will show you how to configure your network settings using a graphical environment and the command line. In section 5.2, "Managing Unix Users and Unix Groups" [page 107], we will talk about users and groups, showing you how to create and modify user accounts, set passwords, disable accounts, and manage groups. Finally, we will discuss services in section 5.3, "Configuring Services" [page 109] and explain how to set up and maintain generic services and also focus on three very important and specific services: SSH, PostgreSQL, and Apache.

## 5.1. Configuring the Network

### 5.1.1. On the Desktop with *NetworkManager*

In a typical desktop installation, you'll have *NetworkManager* already installed and it can be controlled and configured through GNOME's control center and through the top-right menu as shown in Figure 5.1, "Network Configuration Screen" [page 104].

![](img/46e3313ea1bb2892f314630a4f0677b8_130_0.png)

The default network configuration relies on DHCP to obtain an IP address, DNS server, and gateway, but you can use the gear icon in the lower-right corner to alter the configuration in many ways (for example: set the MAC address, switch to a static setup, enable or disable IPv6, and add additional routes). You can create profiles to save multiple wired network configurations and easily switch between them. For wireless networks, their settings are automatically tied to their public identifier (SSID).

NetworkManager also handles connections by mobile broadband (Wireless Wide Area Network WWAN) and by modems using point-to-point protocol over ethernet (PPPoE). Last but not least, it provides integration with many types of virtual private networks (VPN) through dedicated plugins: SSH, OpenVPN, Cisco's VPN C, PPTP, Strogswan. Check out the `network-manager-*` packages; most of them are not installed by default. Note that you need the packages suffixed with `-gnome` to be able to configure them through the graphical user interface.

### 5.1.2. On the Command Line with ifupdown

Alternatively, when you prefer not to use (or don't have access to) a graphical desktop, you can configure the network with the already-installed `ifupdown` package, which includes the `ifup` and `ifdown` tools. These tools read definitions from the `/etc/network/interfaces` configuration file and are at the heart of the `/etc/init.d/networking` init script that configures the network at boot time.

Each network device managed by `ifupdown` can be deconfigured at any time with `ifdown network-device`. You can then modify `/etc/network/interfaces` and bring the network back up (with the new configuration) with `ifup network-device`.

Let's take a look at what we can put in ifupdown's configuration file. There are two main directives: `auto network-device`, which tells `ifupdown` to automatically configure the network interface once it is available, and `iface network-device inet/inet6 type` to configure a given interface. For example, a plain DHCP configuration looks like this:

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```

Note that the special configuration for the loopback device should always be present in this file. For a fixed IP address configuration, you have to provide more details such as the IP address, the network, and the IP of the gateway:

```
auto eth0
iface eth0 inet static
    address 192.168.0.3
    netmask 255.255.255.0
    broadcast 192.168.0.255
    network 192.168.0.0
    gateway 192.168.0.1
```

For wireless interfaces, you must have the **wpa_supplicant** package (included in Kali by default), which provides many *wpa-**- options that can be used in `/etc/network/interfaces`. Have a look at `/usr/share/doc/wpa_supplicant/README.Debian.gz` for examples and explanations. The most common options are **wpa-ssid** (which defines the name of the wireless network to join) and **wpa-psk** (which defines the passphrase or the key protecting the network).

```
iface wlan0 inet dhcp
    wpa-ssid MyNetWork
    wpa-psk plaintextsecret
```

### 5.1.3. On the Command Line with *systemd-networkd*

While *ifupdown* is the historical tool used by Debian, and while it is still the default for server or other minimal installations, there is a newer tool worth considering: *systemd-networkd*. Its integration with the *systemd* init system makes it a very attractive choice. It is not specific to Debian-based distributions (contrary to *ifupdown*) and has been designed to be very small, efficient, and relatively easy to configure if you understand the syntax of *systemd* unit files. This is an especially attractive choice if you consider *NetworkManager* bloated and hard to configure.

You configure *systemd-networkd* by placing `.network` files into the `/etc/systemd/network/` directory. Alternatively, you can use `/lib/systemd/network/` for packaged files or `/run/systemd/network/` for files generated at run-time. The format of those files is documented in *systemd-networkd(5)*. The **Match** section indicates the network interfaces the configuration applies to. You can specify the interface in many ways, including by media access control (MAC) address or device type. The **Network** section defines the network configuration.

> **Example 5.1** *DHCP-based Configuration in /etc/systemd/network/80-dhcp.network*

```
[Match]
Name=en*

[Network]
DHCP=yes
```

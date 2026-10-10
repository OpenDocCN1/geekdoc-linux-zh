
do to get the job done. Actual configuration can be done using either the automatic DHCP tool or static IP addresses. Linux’s underlying network configuration mechanisms rely on startup scripts and their configuration files, but you may be able to use GUI tools to do the job instead.

## Network Hardware Configuration

The most fundamental part of network configuration is getting the network hardware up and running. In most cases, this task is fairly automatic—most distributions ship with system startup scripts that autodetect the network card and load the correct driver module. If you recompile your kernel, building the correct driver into the main kernel file will also ensure that it’s loaded at system startup.

If your network hardware isn’t correctly detected, though, subsequent configuration (as described in the upcoming sections “DHCP Configuration” and “Static IP Address Configuration”) won’t work. To correct this problem, you must load your network hardware driver. You can do this with the `modprobe` command:

```
# modprobe tulip
```

You must know the name of your network hardware’s kernel module, though (tulip in this example). This name may not be immediately obvious, because it varies greatly depending on your hardware, and the name is usually based on the chipset used in the network card, rather than on the name of the network card or its manufacturer. Chapter 1 includes information on identifying hardware, so consult it if you have problems with this task.

Once Linux has recognized the network hardware, you should be able to continue with network configuration, as described in the next couple of sections. To make Linux recognize your hardware at every boot, though, you may need to add the `modprobe` command to a startup script. This task can be tricky; most distributions use very convoluted startup scripts. These scripts should already be detecting and loading the network driver. If they don’t, the best approach may be to recompile the kernel and build the driver into the main kernel file. Alternatively, you can try adding a call to `modprobe` to an appropriate network startup script; however, placing this call in a good location can be a difficult task. Chapter 4, “Managing System Services,” includes information on system startup scripts.

## Setting Wireless Options

If you’re using a wireless (Wi-Fi) device, you must use the `iwconfig` command to set wireless-specific options before you use DHCP or manual tools to bring up the network interface. This is necessary because wireless networks have their own unique features, such as network names, broadcast frequencies, and encryption keys, that are not applicable to wired networks. As with other network configuration tools, your distribution’s startup scripts may launch `iwconfig` as part of a general network startup routine, so you may not need to do this manually; however, at the very least you’ll need to enter the relevant information in a GUI or text-based tool, perhaps when you install Linux.

To begin the process, you must first obtain information on your wireless network's settings. If you're using a wireless network set up by somebody else, such as your employer's network or a public access point, you should be able to get the relevant information from its maintainer. If you're using a network that you maintain yourself, such as a home network or one that you've set up for your employer, you can find the information from the configuration tools provided by your WAP or broadband router. This information can often be accessed via a Web server run on the device. For instance, Figure 8.3 shows the configuration screen for one broadband router. In this model, the Wireless options screen contains several tabs, each of which provides certain data. Pay particular attention to the radio band (802.11g in Figure 8.3), service set identifier (SSID; NoWires in Figure 8.3), channel (Channel 1 in Figure 8.3), authentication type, and authentication key. (These last two items are on the Security tab, which isn't shown in Figure 8.3.)

### FIGURE 8.3 WAPs and broadband routers provide configuration tools in which you set wireless options for your network.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_406_0.png)

**WARNING** If you're configuring your own wireless network, be sure to enable the highest security level possible: Wi-Fi Protected Access 2 (WPA2). Earlier security systems, and particularly Wired Equivalent Privacy (WEP), are extremely vulnerable. Using them enables anybody with modest skill to snoop on all your network traffic. Depending on your local security settings, intruders might be able to easily break into other wired or wireless computers on your network from outside your building using a notebook computer.

To use **iwconfig**, you pass it the relevant data using option names such as **ssid** and **channel**, preceded by the wireless network device name (typically **wlan0**):

```
# iwconfig wlan0 ssid NoWires channel 1 mode Managed key s:N1mP7miNww
```

This example sets the options for **wlan0** to use the managed network on channel 1 with the SSID of **NoWires** and a password of **N1mP7miNww**. The password requires a few extra comments. Ordinarily, **iwconfig** takes a password as a string of hexadecimal values, with optional dashes between 2-byte blocks, as in 0123-4567-89AB. Often, however, the password is given as a text string. The string *s:* must precede the password in this case, as shown in the example.

For details on additional **iwconfig** options, including some highly technical ones, consult its man page.

Once you’ve configured a wireless interface, you can check on its settings by using **iwconfig** with no options or with only the interface name:

```
# iwconfig wlan0
wlan0	IEEE 802.11g  ESSID: 'NoWires'
	Mode:Managed  Frequency:2.462 GHz  Access Point: 08:10:74:24:1B:D4
	Bit Rate=54 Mb/s  Tx-Power=27 dBm
	Retry min limit:7  RTS thr:off  Fragment thr=2352 B
	Encryption key: 314E-506D-6d37-4E48-0A [2]
	Link Quality=100/100  Signal level=-32 dBm  Noise level=-94 dBm
	Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
	Tx excessive retries:0  Invalid misc:0  Missed beacon:0
```

In addition to providing information on settings, **iwconfig** provides some diagnostic information, such as the link quality, received (Rx) and transmitted (Tx) errors, and so on.

## DHCP Configuration

One of the easiest ways to configure a computer to use a TCP/IP network is to use **DHCP**, which enables one computer on a network to manage the settings for many other computers. It works like this: when a computer running a **DHCP** client boots up, it sends a broadcast in search of a DHCP server. The server replies (using nothing but the client’s hardware address) with the configuration information needed for the client to allow it to communicate with other computers on the network—most importantly the client’s IP address and netmask and the network’s gateway and DNS server addresses. The DHCP server may also give the client a hostname. The client then configures itself with these parameters. The IP address is not assigned permanently; it’s referred to as a *DHCP lease*, and if it’s not renewed, the DHCP server may give the lease to another computer. Therefore, from time to time, the client checks back with the DHCP server to renew its lease.

Three DHCP clients are in common use on Linux: **pump**, **dhclient**, and **dhcpcd** (not to be confused with the DHCP server, **dhcpd**). Some Linux distributions ship with just one of these, but others ship with two or even all three. All distributions have a default DHCP client, though—the one that's installed when you tell the system you want to use DHCP at system installation time. Those that ship with multiple DHCP clients typically enable you to swap out one for another simply by removing the old package and installing the new one.

Ideally, the DHCP client runs at system bootup. This is usually handled either by a SysV startup file, as described in Chapter 4, or as part of the main network configuration startup file (typically a SysV startup file called *network* or *networking*). The system often uses a line in a configuration file to determine whether to run a DHCP client. For instance, Fedora Linux sets this option in a file called `/etc/sysconfig/network-scripts/ifcfg-eth0` (this filename may differ if you use something other than a single Ethernet interface). The line in question looks like this:

```
BOOTPROTO=dhcp
```

If the *BOOTPROTO* variable is set to something else, changing it as shown here will configure the system to use DHCP. It's usually easier to use a GUI configuration tool to set this option, however, as described in the upcoming section “Using GUI Configuration Tools.”

In Ubuntu, the equivalent configuration is done in the `/etc/network/interfaces` file, which contains the following line for DHCP configuration on the first Ethernet device:

```
iface eth0 inet dhcp
```

Replacing *dhcp* with *static* in this line changes the system to use a static IP address, but you must then add lines to provide the static IP address and related information. As with Fedora, it may be easier to use a GUI configuration tool.

## Static IP Address Configuration

If a network lacks a DHCP server, you must provide basic network configuration options manually. You can set these options using interactive commands, as described shortly, but to set them in the long term, you adjust a configuration file. Details vary from one distribution to another, so you may have to search through your `/etc` directory to find the appropriate file to make permanent changes. By way of example, I show the files used in Fedora 10 and Ubuntu 8.04. DNS settings are done in the same way in all distributions. Temporary changes can be done using the same tools on any distribution, as well.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_408_0.png)

> If you aren't sure what to enter for the basic networking values (the IP address, network mask, gateway address, and DNS server addresses), you should consult your network administrator. Do not enter random values or values you make up that are similar to those used by other systems on your network. Doing so is unlikely to work at all, and it could conceivably cause a great deal of trouble—say, if you mistakenly use an IP address that's reserved for another computer.

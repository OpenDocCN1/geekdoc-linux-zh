
the case, try retrieving the same file from a Web browser on the same network and make sure your path is correct and your Web server is configured correctly.

Other things that might halt the installation process could be the installer not being able to get a DHCP lease or, as is most often the case, a mistake in the preseed.cfg file. As you will discover, a good preseed file is something you get after a lot of trial and error. When you set an option incorrectly, the installer will simply stop at that point in the install and prompt you for that particular option. As you create more sophisticated preseed.cfg files, you might run through the same install multiple times before you get it exactly right.

The default preseed.cfg will get you started, but where do you go from there? This chapter digs into each of the main configuration categories and explains how to customize the default preseed.cfg file for your needs.

## Networking Options

In my sample preseed.cfg I introduced the following networking options:

```
d-i netcfg/get_hostname string unassigned-hostname
d-i netcfg/get_domain string unassigned-domain
d-i netcfg/choose_interface select auto
d-i netcfg/wireless_wep string
```

The first two options I used on the boot prompt with their aliases hostname and domain to set the hostname and domain, respectively, for this machine. The choose_interface option allows you to choose which network interface to use on the machine for the install. In my case I chose auto, which will pick the first interface that has link, if possible. Instead of choosing auto, you could also set this option to a specific interface, such as eth1. Now if eth1 were a wireless card and your wireless network uses WEP, you could use the wireless_wep option to set the WEP key. Even though I didn’t use a wireless connection in my example, I still set this to a dummy value so I wouldn’t get prompted for a WEP key during the install.

With these default settings the installer will attempt to get all of its network settings via DHCP, which is probably what most administrators want, especially if they intend to install a machine over PXE. However, you might want to statically assign an IP for a machine, and in that case there are a number of preseed options that you will need to use. The following is an example set of preseed options that will set up a network manually:

```
d-i netcfg/disable_dhcp boolean true
d-i netcfg/get_nameservers string 192.168.1.1
d-i netcfg/get_ipaddress string 192.168.1.50
d-i netcfg/get_netmask string 255.255.255.0
d-i netcfg/get_gateway string 192.168.1.1
d-i netcfg/confirm_static boolean true
```

Most of these options are pretty self-explanatory, so you can just replace the IPs listed here with the IPs you want to use for your name server, the IP of the host itself, gateway, and netmask. The disable_dhcp option is what tells the installer to skip DHCP and use the static settings, and confirm_static simply confirms all of the static options you set; otherwise the installer would prompt you to confirm all of the settings in the middle of the install.

> NOTE One downside to installation with DHCP is that on many installs the machine could potentially attempt to get a lease multiple times. When this happens, you will often notice that the actual physical port will also reset. Now, depending on how your networking equipment is configured, it could take longer than 30 seconds (the default DHCP time-out) for the port to come back up because the switch needs to perform spanning tree calculations. I've had installs that seemed to get a lease only one out of ten or more times because of a race for the port to come back up before DHCP timed out. A Red Hat install I had got a new lease three or four times, and it was basically impossible to win the race that many times in a row. If you notice this is the case, you have a few options. For one, you (or your network administrator) can enable PortFast on that particular switch port so that it speeds up the spanning tree calculations, or you can set the netcfg/dhcp_timeout preseed option to a longer value, such as `d-i netcfg/dhcp_timeout string 60`, to set the DHCP time-out to 60 seconds.

There might be some circumstances when you have a preseed file you want to use both on a network with DHCP and on a network without it. There is a way to configure that with preseeding. Combine all of the netcfg

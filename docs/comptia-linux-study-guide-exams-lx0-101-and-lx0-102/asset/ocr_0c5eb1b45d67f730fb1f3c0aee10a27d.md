# Configuring Linux for a Local Network

Now that you know something about how networking functions, the question arises: How do you implement networking in Linux? Most Linux distributions provide you with the means to configure a network connection during system installation. Therefore, chances are good that network configuration already functions on your system. In case it doesn't, though, the following sections summarize what you need to get the job done. Actual configuration can be done using the automatic DHCP tool or static IP addresses. Linux's underlying network configuration mechanisms rely on startup scripts and their configuration files, but you may be able to use GUI tools to do the job instead.

# Network Hardware Configuration

The most fundamental part of network configuration is getting the network hardware up and running. In most cases, this is fairly automatic—most distributions ship with startup scripts that auto-detect the network card and load the correct driver module. If you rebuild your kernel, building the driver into the main kernel file will ensure that it is loaded at startup.

If your network hardware isn't correctly detected, then subsequent configuration (as described in the upcoming sections “Configuring with DHCP” and “Configuring with a Static IP Address”) won't work. To correct this problem, you must load your network hardware driver. You can do this with the following command:

```
# modprobe tu3ip
```

You must know the name of your network hardware kernel module (tu3ip in this example). Chapter 3, “Configuring Hardware,” describes the task of hardware configuration and activation in more detail.

# Configuring with DHCP

One of the easiest ways to configure a computer to use a TCP/IP network is to use DHCP, which enables one computer on a network to manage the settings for many computers. It works like this: When a computer running a DHCP client boots up, it sends a broadcast search for a DHCP server. The server replies (using nothing but the hardware address) with the configuration information the client needs to communicate with other computers on the network—most important, the client's IP address and name the gateway and DNS servers. The DHCP server may also give the client hostname and provide other details about the network. The client then configures itself with these parameters. The IP address isn't assigned permanently; it is referred to as a DHCP lease, and if it's not renewed, the DHCP server may give the lease to another computer. From time to time the client checks back with the DHCP server to renew its lease.

Three DHCP clients are in common use on Linux: pump, dhclient, and dhcpd (not to be confused with the DHCP server, dhcppd). Some Linux distributions ship with just one
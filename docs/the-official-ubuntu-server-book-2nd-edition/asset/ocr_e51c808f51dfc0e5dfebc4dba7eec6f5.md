While each of these services could reside on totally different hosts, for my example I will step you through how to set up each of them, starting with the same default Ubuntu image with the same default settings I have been using so far in this chapter. In this example I will set up a PXE server with an IP address of 10.1.1.5. On this network my gateway router is at 10.1.1.1 and my DNS servers are at 10.1.1.2 and 10.1.1.3.

# DHCP

The first step is to set up a DHCP server that can hand out IP addresses to each installation candidate. First install the dhcp3-server package:

```
```bash
$ sudo apt-get install dhcp3-server
```
```

By default your DHCP server won’t be configured. All you really need to get everything started is a short subnet section in the /etc/dhcp3/dhcpd.conf file. When you open the file with your preferred text editor, you will notice there is a basic skeleton of a configuration there along with many commented-out examples. Just go to the bottom of the file and add the following subnet section:

```
```text
subnet 10.1.1.1 netmask 255.255.255.0 {
    option domain-name-servers 10.1.1.2, 10.1.1.3;
    option routers 10.1.1.1;
    range dynamic-bootp 10.1.1.50 10.1.1.99;
    next-server 10.1.1.5;
    filename "pxelinux.0";
}
```
```

I will go more into overall DHCP configuration in Chapter 5, but here I have told DHCP to answer queries on the 10.1.1.0/255.255.255.0 subnet. I have listed the two DNS servers on that network along with the router to use. The dynamic-bootp line defines the range of IP addresses this DHCP server will hand out. In this case I will hand out addresses between 10.1.1.50 and 10.1.1.99. The next-server line configures the IP address for TFTPd server to use so that any hosts that PXE boots can retrieve their boot loader (in this case this server) via TFTPd. The filename line tells it the name of the file to retrieve. More on that in the next section.
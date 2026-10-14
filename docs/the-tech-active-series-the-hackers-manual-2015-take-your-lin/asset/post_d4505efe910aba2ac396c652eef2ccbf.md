
## Networking:

After introducing you to the building blocks and tools of networking, we're going to put all that knowledge together to create real, working networks.

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_105_0.png)

On the previous pages, we introduced you to the different components of networking – packets, physical connections and logical addressing – along with the tools you need to inspect their operation on your Linux box. This takes you a long way towards being able to effectively work with networks and diagnose problems that you come across. Now we want to show you how these elements combine to create some real networks. We'll start by getting two computers communicating directly with one another, before moving on to demonstrate how you can turn a Linux box into a router. So that you don't need lots of computers, all of this will be done in VirtualBox, but you should be able to apply the same techniques to physical systems as well.

We'll be using CentOS for our examples – it's based on Red Hat Enterprise Linux, and is a popular choice for servers. If you're interested in Ubuntu or other Debian-based distros, (see the Debian-based distributions box, p109). Before we get started with the networking side of things, we first need to build a lab on which to practise. Your first job, then, is to install VirtualBox. This should be in the default repositories of most distributions, so just use whatever package manager your current distribution comes with. Once you've done that, download the CentOS minimal installation disc (www.centos.org). Now, create two new virtual machines in VirtualBox, following our step-by-step guide opposite to ensure you add all the network interfaces necessary to make things work. Then, repeat the above steps for a second VM, making sure it's attached to the same internal network. By creating VMs with two network interfaces as we have, via the default NAT), but will also be able to communicate directly with each other via the internal network we added. This internal network is the equivalent of plugging the two VMs in to the same switch, or running a wire between the two.

The contents of the /etc/sysconfig/network-scripts directory looks intimidating, but if you focus on the ifcfg-ethX files, you'll find there's a lot you can do here.

## Basic networking

With the installation complete on both machines, it's time to get both connected to the internet via the default NAT network. This will give us a chance to get familiar with Red Hat's network configuration files and to refresh some of the information we covered in the previous pages. The first thing to do after your new VM has booted is to switch to the /etc/sysconfig/network-scripts directory. On Red Hat-based distributions, this directory contains the start-up scripts and configurations for every network device connected to your machine. If you followed our step-by-step, you should see two configuration files, ifcfg-eth0 and ifcfg-eth1 (if you're using a different version of Red Hat, it might be ifcfg-em2 and ifcfg-em2 that you see). Eth0 is the first network device on the system, and should refer to Adapter 1 in the VirtualBox configuration – that is the NAT network.

Using Vi, edit ifcfg-eth0, making sure the following lines are present and set to these values:
NM_CONTROLLED="no"
BOOTPROTO="dhcp"
ONBOOT="yes"

The first line stops NetworkManager from controlling this interface – since we're trying to do things manually, its interference could confuse matters, so we turn it off. The second line specifies what protocol it should use to get its IP address. Here, we've specified DHCP, or Dynamic

```
root@Adam /etc/sysconfig/network-scripts
ifcfg-Auto Ethernet  ifdown-post  ifup-plug
ifcfg-Auto Ethernet-1  ifdown-ppp  ifup-ppp
ifcfg-Auto greater...  ifdown-route  ifup-route
ifcfg-Auto...  ifdown-sit  ifup-sit
ifcfg-Auto_LAN...  ifdown-tunnel  ifup-tunnel
ifcfg-Auto_netgear  ifup  ifup-aliases  ifup-wireless
ifcfg-lo  ifup-bnep  init.ipv6-global
ifdown  ifup-eth  keys-Auto...  network-functions
ifdown-bnep  ifup-ippp  keys-Auto...  net.hotplug
ifdown-ippp  ifup-ipsec  network-functions  network-functions-ipv6
ifdown-isdn  ifup-ipx  network-functions  
root@Adam network-scripts#
```

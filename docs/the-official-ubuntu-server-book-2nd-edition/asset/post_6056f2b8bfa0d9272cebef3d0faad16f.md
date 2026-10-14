
You will use this virsh command a lot. In this case it outputs the list of all VMs currently running on this machine. We haven’t set up any yet, but the fact that we got valid output and not an error means that we are ready to proceed. If you got some sort of permissions error, it is likely because your user is not part of the libvirt group.

## Configure KVM Networking

There are two main ways you can set up networking for your VMs. The default networking setup provides a private network under 192.168.122.0/24. A DHCP server will hand out the rest of the IPs; alternatively, you can set up static IPs for your VM. The KVM host has the IP 192.168.122.1, and VMs then communicate with the outside world via that gateway using NAT (Network Address Translation). This works fine, especially for VMs on a desktop, but since we are talking about servers here, my assumption is that you want machines outside of the KVM host to be able to communicate with your VMs. While you could certainly set up some sort of iptables DNAT rules and forward traffic back in, that solution doesn’t scale very well. The real solution is to set up bridged networking so that your VMs appear to be on the same network as your host.

It is relatively simple to set up the br0 bridge interface on Ubuntu. Essentially you identify the interface over which you want to bridge traffic (probably eth0 or possibly bond0 if you set up bonding), transfer all of its configuration to br0 along with a few extra bridge options, and then change the original interface to manual mode. It makes more sense when you see the examples. For instance, if I had DHCP set up for eth0 and my old configuration in /etc/network/interfaces looked like this:

```
auto eth0
iface eth0 inet dhcp
```

then my new configuration would look like this:

```
auto eth0
iface eth0 inet manual

auto br0
```
```
iface br0 inet dhcp
    bridge_ports eth0
    bridge_fd 9
    bridge_hello 2
    bridge_maxage 12
    bridge_stp off
```

Note that I changed the inet mode for eth0 from dhcp to manual. If eth0 had a static IP configured, I would just transfer all that configuration to br0 instead, so it would go from this:

```
auto eth0
iface eth0 inet static
    address 192.168.0.5
    network 192.168.0.0
    netmask 255.255.255.0
    broadcast 192.168.0.255
    gateway 192.168.0.1
```

to this:

```
auto eth0
iface eth0 inet manual

auto br0
iface br0 inet static
    address 192.168.0.5
    network 192.168.0.0
    netmask 255.255.255.0
    broadcast 192.168.0.255
    gateway 192.168.0.1
    bridge_ports eth0
    bridge_fd 9
    bridge_hello 2
    bridge_maxage 12
    bridge_stp off
```

Once I have set up /etc/network/interfaces to have the bridge, I then restart networking:

```
$ sudo /etc/init.d/networking restart
```

Now my ifconfig output should list my new bridged interface:

```
$ ifconfig
br0      Link encap:Ethernet  HWaddr 00:17:42:f1:18:be
          inet addr:192.168.0.5  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::217:42ff:felf:18be/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:17226 errors:0 dropped:0 overruns:0 frame:0
          TX packets:13277 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:16519186 (16.5 MB)  TX bytes:1455348 (1.4 MB)
```

> NOTE Even though we are talking about servers with physical network connections here, I should bring up the fact that most wireless adapters don't support bridging, so if you try to set this up on your laptop and bridge over your wireless interface, bridged mode won't work.

Once the bridge interface is set up, the current KVM installation should be able to take advantage of it by default. Now you are ready to create your first VM.

## Create a New VM

Once KVM and your bridged network are set up, you are ready to create your first VM. Ubuntu has set up a tool called ubuntu-vm-builder (in newer releases renamed vmbuilder) that you can use to automate the process of creating a VM. With vmbuilder you can define the settings for a VM, including what Ubuntu release you want, and the tool will create the local virtual disk and perform the base install for you. It will even register the VM with the system so that it's ready to go once it completes.

To streamline the process even further, Ubuntu has created a special Ubuntu installation known as JeOS (pronounced "juice") for virtual machines. All of the nonessential kernel modules have been removed, and the OS in general is tuned for better performance as a VM. In the examples that follow I create VMs based on JeOS.

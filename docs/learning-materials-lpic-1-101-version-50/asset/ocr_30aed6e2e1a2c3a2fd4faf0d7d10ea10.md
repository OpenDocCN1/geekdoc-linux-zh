hypervisor to emulate hardware devices that the virtual machine will use, such as disk controllers, access to the host CPU, network card emulation, and more.

Note that there is a directory named **networks**. This directory contains definition files (also using XML) that create network configurations that the virtual machines can use. This hypervisor is only using one network, and so there is only one definition file that contains a configuration for a virtual network segment that these systems will utilize.

```
```
$ ls -l /etc/libvirt/qemu/networks/
total 8
drwxr-x 2 root root 4096 Jun 29 17:15 autostart
-rw------ 1 root root  576 Jun 28 16:39 default.xml
$ sudo cat /etc/libvirt/qemu/networks/default.xml
<!--
  WARNING: THIS IS AN AUTO-GENERATED FILE. CHANGES TO IT ARE LIKELY TO BE
  OVERWRITTEN AND LOST. Changes to this xml configuration should be made using:
    virsh net-edit default
  or other application using the libvirt API.
-->

<network>
  <name>default</name>
  <uuid>55ab064f-62f8-49d3-8d25-8ef36a524344</uuid>
  <forward mode='nat'/>
  <bridge name='virbr0' stp='on' delay='0'/>
  <mac address='52:54:00:b8:e0:15'/>
  <ip address='192.168.122.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.122.2' end='192.168.122.254'/>
    </dhcp>
  </ip>
</network>
```
```

This definition includes a Class C private network and an emulated hardware device to act as a router for this network. There is also a range of IP addresses for the hypervisor to use with a DHCP server implementation that can be assigned to the virtual machines that use this network. This network configuration also utilizes network address translation (NAT) to forward packets to other networks, such as the hypervisor’s LAN.

Now we turn our attention to a Red Hat Enterprise Linux 8 virtual machine definition file. (sections of special note are in **bold** text):
# Chapter 24 Virtualization

Under KVM, the Linux kernel itself serves as the hypervisor; memory management and scheduling are handled through the host's kernel, and guest machines are normal Linux processes. Enormous benefits accompany this unique approach to virtualization. For example, the complexity introduced by multiprocessors is handled by the kernel, and no hypervisor is required to support them. Linux commands such as top, ps, and kill show and control virtual machines, just as they would for other processes. The integration with Linux is seamless.

Administrators should be cautioned that KVM is a relatively young technology, and it should be heavily tested before being promoted to production use. The KVM site itself documents numerous incompatibilities when running guests of differing operating system factors. Reports of live migrations breaking between different versions of KVM are common. Consider yourself forearmed.

# KVM installation and usage

Although the technologies used between Xen and KVM are fundamentally different, the tools to install and manage guest operating systems are similar. Under Xen, you can use virt-install to create new KVM guests. Use the virsh command to manage them. These utilities depend on Red Hat's library.

Before the installation is started, the host must be configured to support networking in the guests. In most configurations, one physical interface is used to bridge network connectivity to each of the guests. Under Red Hat, the network device configuration files are in /etc/sysconfig/network-scripts. Two device files are required: one for the bridge and the physical device.

In the examples below, path0 is the physical device and eth0 is the bridge:

```
/etc/sysconfig/network-scripts/path0
DEVICE=eth0
ONBOOT=yes
BRIDGE=eth0
HWADDR=XX.XX.XX.XX:XX:XX
```

```
/etc/sysconfig/network-scripts/eth0
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
TYPE=Bridge
```

Here, the eth0 device receives an IP address through DHCP.

The flags passed to virt-install vary slightly from those used for Xen installation. To begin with, the -hvm flag indicates that the guest should be hardware virtualized, as opposed to paravirtualized. The --connect argument guarantees that the correct default hypervisor is chosen, so virt-install sup

+   5. You can use virsh to manage Xen DomUs as if you wish.
6. This is equally true with Xen, and xend does the heavy lifting, creating interfaces in the background.
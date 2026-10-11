
- **domid**. A numeric, consecutive domain ID, which is automatically assigned when the domain starts.
- **memory**. The amount of memory assigned to the domain.
- **vcpus**. The number of virtual CPUs utilized by this domain.
- **state**. The current state of the domain. This could be:
    - **r**. The domain is running.
    - **b**. The domain has been created, but is currently blocked. This can happen, when a domain is waiting for I/O or when there is nothing to do for the domain.
    - **p**. The domain is paused. The state of the domain is saved and can be restored.
    - **s**. The domain is in the process of being shutdown.
    - **c**. The domain is crashed, due to an error or misconfiguration.

An alternative to list is the command **top**, which displays domain information updated in real-time.

The **console** command connects you with the terminal of a running domain:

```
xm console <domain_id>
```

The command takes the domain id as a parameter, which can be determined with the **list** command (field domid). As mentioned before, use the key combination **Ctrl-J** to disconnect from a terminal.

With the **pause** command you can interrupt the execution of a domain temporarily:

```
xm pause <domain_id>
```

A paused domain is not completely shut down. The current state is saved and the execution of the domain can be continued with the **unpause** command:

```
xm unpause <domain_id>
```

To shutdown a domain, use the **shutdown** command:

```
xm shutdown <domain_id>
```

In case the domain is not responding anymore, you can force the shutdown of the domain with the **destroy** command:

```
xm destroy <domain_id>
```

To save the state of a domain for a longer time (e.g. over a reboot of domain0) you can use the **save** command:

```
xm save <domain_id> <filename>
```

The domain can be restored from the resulting file with the **restore** command:

```
xm restore <filename>
```

Another commonly used command is **mem-set**, which allows you to change the memory allocation of a domain:

```
xm mem_set <domain_id> <amount_of_memory>
```

The amount of memory is specified in megabytes.

> Instead of the domain ID <domain_id>, you can also use the domain name in all xm commands.

### Exercise 8-3
### Change Memory Allocation of a Guest Domain

In the following you learn how to change the memory allocation of a guest domain by changing the domain configuration file.

You can find this exercise in the workbook.

(End of Exercise)

## Automate Domain Startup and Shutdown

When you start, shutdown or reboot domain0 of a Xen system, this also affects the other running Xen domains. Without a running domain0, the other Xen domains cannot operate.

SUSE Linux Enterprise Server 10 comes with a start script called **xendomains** which is included in the package **xen-tools**.

The script should be installed on domain0 and does the following:

- When domain0 is booted, all domains with configuration files located under /etc/xen/auto/ are started.
- When domain0 is shutdown or rebooted, running Xen domains are shutdown automatically.

The script has some configuration options, which can be adjusted in the file /etc/sysconfig/xendomains. The configuration variables in this file are well documented.

One interesting option is to migrate domains automatically to a different host when a domain0 is shutdown. This can be configured in the variable **XENDOMAINS_MIGRATE**. The variable has to be set to the IP address of the target machine. When the variable is empty, no migration is performed.

## Manage Virtualization with Xen

### Exercise 8-4
### Automate Domain Startup

In this exercise, you learn how to startup domains automatically when the system is booted.

You can find this exercise in the workbook.

(End of Exercise)

## Objective 6: Understand Xen Networking

Usually the network connection of Xen domains works out of the box. However, in case you would like to change the configuration, networking with Xen can be a bit tricky. The following should give you an overview of how Xen domains are connected to the physical network.

To better understand the concept of Xen networking, do the following:

- Understand the Basic Networking Concept
- Understand Bridging
- Understand the Network Interfaces in domain0

### Understand the Basic Networking Concept

In a Xen setup, domain0 is controlling the physical network interfaces of a host system. Unprivileged domains are connected to domain0 through virtual ethernet adapters.

One virtual adapter in an unprivileged domain is connected to one virtual adapter in domain0.

In domain0, standard Linux networking mechanisms like bridging or routing are used to connect the virtual adapters through the physical adapter to the network.

The following is an illustration of this basic concept:

#### Figure 8-10

![](img/63e88022bf135307e3eac051ad238b5b_398_0.png)

### Understand Bridging

On SUSE Linux Enterprise Server 10, the default mechanism to connect virtual and physical interfaces in domain0 is bridging. Other mechanisms like routing with or without Network Address Translation (NAT) are out of the scope of this course.

Bridging basically means that multiple network interfaces are combined to one. Traditionally this technique is used to connect two physical network interfaces or network segments.

In a Xen system, bridging is used to connect virtual and physical network adapters in domain0. In a Xen system, you can consider the bridge as a kind of virtual switch which all virtual and physical interfaces are connected to.

The configuration of the bridge is done by the xend management process. When a new domain is created, the following changes to the network configuration are made (simplified):

1. Xen provides a virtual interface to the new domain.
2. xend creates a new virtual interface in domain0.
3. Both virtual interfaces are connected through a virtual point to point connection.
4. The virtual interface in domain0 is added to the bridge with the physical interface.

These steps only affect the general network connectivity. The IP configuration in the Xen domains has to be done separately with DHCP or a static network configuration.

xend is performing these network changes with the help of scripts, which are located at /etc/xen/scripts/. The following scripts are used for bridged networking:

- network-bridge. This script is called initially when xend is started. It sets up the bridge xenbr0 and moves the physical interfaces onto that bridge.
- vif-bridge. This script is called for every domain that is started and adds the virtual interface to the bridge.

In the file /etc/xen/xend-config.sxp you can configure which network scripts are used by xend.

### Understand the Network Interfaces in domain0

When you look at the network interfaces in domain0 with the command ip a, you can see that there are many more interfaces than in a regular Linux installation.

The following is an example output of `ip a` on domain0 (shortened):

```
linux-3rsm:~ # ip a
1: lo: <LOOPBACK,UP> mtu 16436 qdisc noqueue
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    inet6 ::1/128 scope host
    valid_lft forever preferred_lft forever
2: peth0: <BROADCAST,MULTICAST,NOARP,UP> mtu 1500 qdisc pfifo_fast qlen 100
    link/ether fe:ff:ff:ff:fe:ff brd ff:ff:ff:ff:ff:ff
    inet6 fe80::fcff:feff:feff:64 scope link
    valid_lft forever preferred_lft forever
4: vif0.0: <BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue
    link/ether fe:ff:ff:fe:ff brd ff:ff:ff:ff:ff:ff
    inet6 fe80::fcff:feff:feff:64 scope link
    valid_lft forever preferred_lft forever
5: eth0: <BROADCAST,MULTICAST,NOTRAILERS,UP> mtu 1500 qdisc noqueue
    link/ether 00:11:25:81:4c:5b brd ff:ff:ff:ff:ff:ff
    inet 149.44.171.67/23 brd 149.44.171.255 scope global eth0
    inet6 2001:780:101:aa00:211:25e5:fe81:4c5b/64 scope global dynamic
    valid_lft 29998sec preferred_lft 9998sec
    inet6 fe80::211:25e5:fe81:4c5b/64 scope link
    valid_lft forever preferred_lft forever
6: vif0.1: <BROADCAST,MULTICAST> mtu 1500 qdisc noop
    link/ether fe:ff:ff:fe:ff brd ff:ff:ff:ff:ff:ff
7: veth1: <BROADCAST,MULTICAST> mtu 1500 qdisc noop
    link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
    [...]
19: veth7: <BROADCAST,MULTICAST> mtu 1500 qdisc noop
    link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
20: xenbr0: <BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue
    link/ether fe:ff:ff:fe:ff brd ff:ff:ff:ff:ff:ff
    inet6 2001:780:101:aa00:fcff:feff:feff:feff/64 scope global dynamic
    valid_lft 29998sec preferred_lft 9998sec
    inet6 fe80::200:fe:fe00:0/64 scope link
    valid_lft forever preferred_lft forever
23: vif3.0: <BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue
    link/ether fe:ff:ff:fe:ff brd ff:ff:ff:ff:ff:ff
    inet6 fe80:::c:fcff:feff:feff:64 scope link
    valid_lft forever preferred_lft forever
```

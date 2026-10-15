
it could trigger events that parts of the operating system or external applications work on to dispose of the packets.

The OpenBSD UNIX implementation of packet filtering, named PF, is available in the base FreeBSD, PC-BSD systems, and Solaris. PF lets you write filtering rules to control network traffic based on essentially any packet or connection property, including address family, source and destination address, interface, protocol, port, and direction.

A packet filter can keep unwanted traffic out of your individual computer or network-connected computers. It can also help keep network traffic inside your own network. Both these functions are important to the firewall concept, but blocking is not the only useful feature of a packet filter.

Filtering can also be used to direct specific network traffic to specific hosts, assign classes of traffic to queues, perform traffic shaping, and dispose of selected kinds of traffic to other software for special treatment.

All this processing happens at the network level, based on packet and connection properties. PF is part of the network stack, firmly embedded in the operating system kernel. The filtering is performed in the kernel because of performance considerations. One of the most important and common actions that PF performs is to block traffic.

## PF on PC-BSD

To enable PF on PC-BSD, do the following:

- 1. Edit your /etc/rc_conf to include the following lines:

```
pf_enable="YES"          # Enable PF (load module if required)
pflog_enable="YES"       # start pflogd(8)
At this point, you may have to reboot the computer.
```

- 2. Enable PF with the following command. If PF is already enabled, go to step 3:

```
% sudo pfctl -e
```

- 3. On FreeBSD and PC-BSD base systems, the /etc/rc.d/pf script requires at least a line in /etc/rc.conf that reads pf_enable="YES" and a valid /etc/pf.conf file. If either of these requirements isn't met, the script will exit with an error message. There is no /etc/pf.conf file in a default FreeBSD and PC-BSD installation, so you'll need to create one before you reboot the system with PF enabled. You can create an empty /etc/pf.conf with touch or could also work from a copy of the /usr/share/examples/pf.conf file supplied by the system.

- 4. With the lines from step 1 in your /etc/rc.conf and created an /etc/pf.conf file, you could also use the PF rc script to run PF. The following starts the PF daemon:

```
% sudo /etc/rc.d/pf start
```

- 5. Use the pfctl command to modify the behavior of PF—for example, to add or modify packet filter rules.

- 6. To stop the PF daemon, use the following command:

```
%sudo /etc/rc.d/pf stop
```

## PF on Solaris

To run PF as your firewall on Solaris, you first install the PF firewall package, and then configure the firewall to reflect your policy. Once configured, you then enable the firewall service. The PF firewall package can coexist with the IP Filter (ipfilter) package that is preinstalled and enabled by default. However, only one firewall at a time can be enabled on a Solaris system!

To install and configure the PF firewall package, you must become the superuser. The following steps allow you to install, configure, and make the PF firewall the active packet filtering software:

- 1. Install the PF package with the following command:

```
# pkg install firewall
```

- 2. Create or update your packet filtering rule set by using the pfconf script with the command:

```
# pfconf
```

The pfconf script modifies the pf.conf PF configuration file.

Use the pfctl command to modify the behavior of PF—for example, to add or modify packet filter rules.

- 3. Disable the ipfilter service first, then enable PF. This is critical, because you don't want two active firewall programs with conflicting rules. Use the svcadm command to accomplish this as follows:

```
# svcadm disable network/ipfilter
# svcadm enable network/firewall
```

If the PF configuration file is empty and you enable the firewall service, some traffic filtering occurs. For example, PF drops TCP packets with invalid flag combinations.

- 4. (Optional) To disable the service, use the svcadm command:

```
# svcadm disable network/firewall
```

This command removes all rules from the kernel and disables the service.

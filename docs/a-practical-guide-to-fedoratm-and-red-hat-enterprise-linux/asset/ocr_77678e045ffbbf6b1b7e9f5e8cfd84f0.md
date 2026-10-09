# THE **FIREWALLD SERVICE**

The **firewalld** service (which uses the **firewalld** daemon) is replacing the **iptables** service. As contrasted with the **iptables** service, the **firewalld** service does not need to be reloaded with every change; it accepts changes to the firewall while it is running. Reloading the **iptables** service frequently breaks established connections. Nowhere is this problem more evident than with virtualization because the firewall changes each time a VM is brought up or down. The **libvirt** library (page 662) now uses **firewalld** to adjust the firewall as needed.

A firewall set up under **firewalld** must be managed directly by the **firewalld** daemon so that the state in the daemon and the state in the kernel remain in sync. Thus you cannot use **iptables** commands to add rules to a firewall controlled by **firewalld**.

The **firewalld** daemon introduces a level of abstraction that makes setting up a firewall simpler and more intuitive. Instead of writing firewall rules as **iptables** requires, with **firewalld** you use *firewall-config* (GUI) or *firewall-cmd* (CLI) to set up a firewall.

The **firewalld** daemon is managed by systemd (page 438) using the **firewalld.service** unit. It is started before networking so that it can immediately protect the network when the network is brought up.

Running in *kernelspace* (page 1257), *netfilter* is a set of tables that hold rules the kernel uses to control network packet filtering. To be useful, *netfilter* requires a front end. The **firewalld** front end runs in *userspace* (page 1279) and enables an administrator to set up a firewall (just as **iptables** does).

D-BUS (www.freedesktop.org/wiki/Software/DBus) is an IPC (interprocess communication system), also called a message bus system, that allows applications and processes to talk with one another and request services over a bus. The **dbus** service (which runs **dbus-daemon**) notifies processes of events (e.g., when a new device is added or when a user logs in).

The **firewalld** daemon has a D-BUS interface that allows it to communicate with processes. Applications, daemons, and administrators can enable/disable a **firewalld** feature using D-BUS. These features can include opening ports, forwarding ports or packets, and performing more advanced tasks.

# **FIREWALLD CONFIGURATION**

This section describes some aspects of the **firewalld** configuration.

# RUNTIME VERSUS PERMANENT CONFIGURATION

When you set up or change a **firewalld** feature, you can do so in the runtime configuration, which causes the change to be made immediately on the running system. Or you can make the change in the permanent (persistent) configuration, which takes effect when the firewall is reloaded or when the system is rebooted.
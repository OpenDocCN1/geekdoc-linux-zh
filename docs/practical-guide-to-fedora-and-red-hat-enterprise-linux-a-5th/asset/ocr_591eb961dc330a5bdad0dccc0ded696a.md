# # PREREQUISITES

Install the following package:

+   - **iptables**

Run `chkconfig` to cause **iptables** to start when the system comes up:

```
`# /sbin/chkconfig iptables on`
```

To ensure maximum protection, the **iptables** init script starts packet filtering by running **iptables** very soon after the system enters runlevels 2-5; in contrast, this script does not stop packet filtering almost until the system leaves runlevels 0, 1, and 6. See page 426 for more information on init scripts.

# # NOTES

The **iptables** utility differs from most other Linux utilities in its setup and use. Whereas other Linux utilities such as Apacne, **vsftpd**, and **sshd** read the data that controls their operation from a configuration file, **iptables** requires you to give a series of **iptables** commands to build a set of packet filtering rules that are kept in the kernel.

There are two ways to set up the same set of rules each time you bring the system up. First, you can put **iptables** commands in a script and run that script each time the system boots. You can call this script from `/etc/rc.d/rc.local`.

Second, you can put the arguments to the **iptables** commands you want to execute in `/etc/sysconfig/iptables`. The *system-config-firewall* utility (page 833) and the Anaconda installer (page 57) both use this technique, building sets of rules and storing the corresponding **iptables** command arguments in `/etc/sysconfig/iptables`. The command `service iptables save` stores the **iptables** rules currently in effect to this file. If you use the `/etc/sysconfig/iptables` file in this manner, be aware that *system-config-firewall* and `service iptables save` overwrite this file.

For information on copying packet filtering rules to and from the kernel, refer to “Copying Rules to and from the Kernel” on page 832. You can run **iptables** with the `-L` option or you can run `service iptables status` to display the packet filtering rules the kernel is using.

The **iptables** init script executes the `/etc/sysconfig/iptables-config` file. Refer to the comments in this file for options you can set in it.

If you encounter problems related to the firewall rules, you can return packet processing rules in the kernel to their default state without rebooting by giving the following commands:

```
`# iptables --flush && iptables --delete-chain`
```

These commands flush all chains and delete any user-defined chains, leaving the system without a firewall. In an emergency you can give the following command to unload all **iptables** modules from the kernel and set a policy of DROP for all tables:

```
`# /sbin/service iptables panic`
```

Resetting **iptables**
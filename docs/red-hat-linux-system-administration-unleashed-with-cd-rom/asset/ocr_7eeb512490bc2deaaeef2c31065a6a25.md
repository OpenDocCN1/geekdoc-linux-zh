# Turning On IP Forwarding

Once the new kernel is in place and the system is back up and running, you will need to turn on IP forwarding. Although it was selected in the kernel configuration, by default it is turned off. To turn on packet forwarding, edit the file /etc/sysconfig/network and change the parameter FORWARD_IPV4 from false to true. This will turn on IP forwarding every time you reboot your system.

Next, the firewall rules need to be put into place. The filters will need to be defined at the appropriate time as the system comes up. The best place to start the firewall is just before the network devices are configured using ifconfig. Under Red Hat Linux, the interfaces are configured in the /etc/rc.d/init.d/network script. This script tends to be one of the first scripts executed in run levels 2, 3, and 5. In these run-level directories, the symbolic link for the /etc/rc.d/init.d/network shell program is S10network. One possible method of setting the packet filtering rules in place before the interfaces are configured is to create a shell script such as /etc/rc.d/init.d/firewalls. Then create the links in the run-level directories with the following command:

```
# for i in rc2.d,rc3.d,rc5.d ; do
# cd /etc/rc.d/$i
# ln -s ../init.d/firewalls S5firewalls
# cd ..
# done
```

This little shell loop changes directory into each of the rc2.d, rc3.d, and rc5.d run-level directories and creates a link to the firewall shell program in /etc/rc.d/init.d/ that will run before the network will be brought up. This prevents any window where a network interface may be active but not controlled by the firewall.

The shell program /etc/rc.d/init.d/firewalls is a simple bourne shell program and is shown in Listing 26.2. This script assumes the following network topology:

Firewall Host: fw1.fwcorp.com
Interfaces: eth0(internal), eth1(external)
Masquerade: no
eth0: 128.83.137.35
eth1: 128.83.155.44

# LISTING 26.2 Firewall Startup Script

```
#!/bin/bash
#
# S5firewall - a simple firewall script to setup a packet filter using ipwadm
#
#
```
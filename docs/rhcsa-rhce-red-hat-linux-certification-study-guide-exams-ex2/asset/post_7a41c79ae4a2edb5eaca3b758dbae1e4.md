
## EXERCISE 5-4
### Revise Network Interfaces on a Cloned System

Now that you know something of networking on a RHEL system, you're ready to modify the network interfaces on a cloned system. Since cloned systems originally have the same network interfaces as the original, they should be changed before they're connected to a local network. Otherwise, there will be two systems on the same network, declaring their ownership of the same IP addresses. And that would be trouble for both systems.

These instructions assume that you want to set up the cloned system as the outsider1.example.org system described in Chapter 1, with an IP address of 192.168.100.100, on the 192.168.100.0/24 network. If an outsider1.example.org system already exists, you can substitute a different system name on a different IP address. (Some home network devices such as cable modems are configured on the 192.168.100.0 network. In that case, you may need to use a different network address.)

If you've set up a cloned system on a virtual machine such as KVM, the first steps involve deleting the current network card and creating a new network card. As this book is modeled on KVM-based virtual machines, the steps are based on that system. While not tested, the same principles should help you reconfigure networking on a cloned system on a different type of virtual machine such as KVM.

- 1. Open the Virtual Machine Manager with the `virt-manager` command.
- 2. Connect to the system with the target virtual machines, normally **localhost** (QEMU).
- 3. Click Edit | Host Details, and click the Virtual Networks tab.
- 4. Select Add (which may be a plus sign). Follow the prompts to create the new virtual network, including the IP address range given. Call this the **outside** network (or another name of your choice). Do not delete the current default network; both networks are required. Traffic between the two networks can be routed through the physical host system.
- 5. Configure the system to forward information to the physical network, using Network Address Translation (NAT). The result should look like the illustration.

![](img/9139201cfcaf4292284a0eed074928e5_309_0.png)

- 6. Return to the main Virtual Machine Manager window. Select the cloned system. Click View | Details.
- 7. Select the current network device and click Remove.
- 8. Click Add Hardware, select the Network hardware type, select the outside network, and create the new network card.
- 9. Click View | Console. Boot the cloned system into runlevel 1, which should not start networking.
- 10. Edit the /etc/sysconfig/network file. Be sure to make a change to the HOSTNAME directive, in this case to outsider1.example.org.
- 11. Examine the /etc/sysconfig/network-scripts/ifcfg-eth0 file. Don't make any changes yet. Since you've changed network cards, the system will detect it and use the next available network device.
- 12. Move to runlevel 3 with a command like `telinit 3`. Unless you've made some unusual changes, that should start networking.
- 13. Run the **ifconfig -a** command. It'll display the detected Ethernet device, along with its hardware address. The detected Ethernet device will be different from eth0, perhaps eth1. You'll need both pieces of information, along with the desired IP address information described earlier.
- 14. Open the **/etc/sysconfig/network-scripts/ifcfg-eth0** file. Make appropriate changes to the **DEVICE**, the various IP addresses, and the **HWADDR** directives.
- 15. Apply the **cp** or **mv** commands to the ifcfg-eth0 file. The new name should reflect the new Ethernet device, such as ifcfg-eth1 for the eth1 device.
- 16. Copy the resulting file to the **/etc/sysconfig/networking/devices** and **/etc/sysconfig/networking/profiles/default** directories.
- 17. Restart networking with the **/etc/sysconfig/network** restart command.
- 18. Verify the network device and routing table have the right settings with the **ifconfig** and **route -n** commands.

Assuming IP Forwarding has been enabled on the physical host system, and there are no blocks such as firewall rules, the virtual machines should now all be able to communicate with outside networks. In Chapter 10, you'll explore how to set appropriate IP forwarding rules based on **iptables** commands documented in the **/etc/sysconfig/iptables** file. For more information on firewalls and IP Forwarding, see Chapters 4 and 10, respectively. If you're studying only for the RHCSA exam, open the **/etc/sysctl.conf** file, make sure to set **net.ipv4.ip_forward=1** and run the `sysctl -p` command.

## CERTIFICATION OBJECTIVE 5.06
### Time Synchronization

The configuration of a Network Time Protocol (NTP) client is straightforward. While it's no longer part of the RHCSA objectives, it's still part of one of the prep courses for the RHCSA, RH124. It would be easy for Red Hat to include this topic as part of future RHCSA objectives. Therefore, this section provides a minimal overview of the client files and the associated GUI configuration tool.

There are good reasons to keep different systems running on the same clock. Otherwise, one system that may take web orders may miss the lack of inventory from a second system that manages a warehouse database, or even see out-of-date production figures from a third system associated with a manufacturing assembly line.

## An NTP Client

Every system, real or virtual, starts with a hardware clock. The time on that clock may depend on the power in a battery; over time, batteries lose power and many hardware clocks end up losing time. The installation process on RHEL 6 normally sets the hardware clock to UTC, which is essentially identical to Greenwich Mean Time (GMT). Linux bases time changes such as Daylight Saving Time on the use of UTC.

Every RHEL 6 system includes a time zone configured in the /etc/sysconfig/clock file. The contents are simple; a typical system may include the following line:

```
ZONE="America/Los_Angeles"
```

The default NTP configuration file, /etc/ntp.conf, is set up to connect to standard Red Hat servers that are part of the NTP pool project. Collectively, any errors from these servers relative to actual time is minimized.

```
server 0.rhel.pool.ntp.org
server 1.rhel.pool.ntp.org
server 2.rhel.pool.ntp.org
```

Users of rebuild distributions such as CentOS will see different Universal Resource Identifiers (URIs), such as 0.centos.pool.ntp.org.

## Date/Time Properties

With the Date/Time Properties configuration tool, you can set the date, time, time zone, and NTP server for the local system. To start it in the GUI, run the `system-config-date` command. This opens the Date/Time Properties window shown in Figure 5-15.

You should recognize the URLs for the NTP servers as the pool servers previously discussed. In other words, the Date/Time Properties tool is a front end for editing the /etc/ntp.conf file. The advanced option to Speed Up Initial Synchronization minimizes the time lag effect of polling multiple NTP servers. The Use Local Time

## FIGURE 5-15
Date/Time Properties tool

![](img/9139201cfcaf4292284a0eed074928e5_312_0.png)

Source directive uses the local system as its own server. The Time Zone tab supports changes to the local time zone, handy for users who travel.

## CERTIFICATION SUMMARY

This chapter covered the basic boot process of a RHEL system. It starts with the hardware POST and continues with the BIOS or UEFI systems. Once it finds boot media, it moves to the first stage of the GRUB bootloader. The GRUB menu allows you to select and customize the kernel to be booted. GRUB can be secured, as it supports booting into different runlevels, including a runlevel which supports root-level access without a user password.

Once you've selected an option from GRUB, it hands control to the kernel. It starts with a temporary filesystem known as the Initial RAM disk. Once essential drivers and filesystems are loaded, you can find out more about what happens through /var/log/dmesg and the drivers it loads. It hands control to the First Process,

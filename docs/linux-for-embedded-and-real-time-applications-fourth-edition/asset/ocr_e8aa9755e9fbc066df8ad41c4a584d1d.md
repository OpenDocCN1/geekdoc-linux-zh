Type <Enter> to exit Modem and dialing, and then select Screen and keyboard. Type “B” once to change the Backspace key from BS to DEL.

Type <Enter> to exit Screen and keyboard. Select Save setup as dfl (default). Then select Exit.

At this point, /dev/ttyACM0 does not exist because you have not powered up the target. But if it did exist, you would see that only the owner and group have access to the device. In order to gain access to this port, you must become a member of the dialout group.

There used to be a nice graphical dialog accessible from the Start menu under Administration>Users and Groups that made this process very easy. Not anymore. Now you have to edit the appropriate file under /etc, in this case group. As root user, open /etc/group in an editor. Find the line that begins “dialout:” and add “:<your_user_name>” at the end of the line. Save the file and close the editor.

# ## Networking

There are a couple of changes needed on the host’s network configuration.

# ### Network Address

Your workstation is probably configured to get a network address via DHCP (Dynamic Host Configuration Protocol). But in this case, to keep things simple, we are going to specify fixed IP addresses for both the workstation and the target.

The CentOS graphical menu for changing network parameters is accessed from Settings -> System Settings3. Select Network Settings and either the Wired or Wireless tab, depending on the nature of your network connection. In the case of a virtual machine, even a wireless interface looks like a wired interface to the guest OS.

Select the network interface and click Edit... Your network interface is probably named something like enp0s8, which means it is an Ethernet device (en) attached to slot 8 of PCI bus segment 0. Change the Method from DHCP to Manual. Now enter the fixed IP address. Network address 192.168.1 is a good choice here, because it is one of a range of network addresses reserved for local networks. Select node 2 for your workstation. The Subnet Mask will be automatically filled in. Fig. 4.2 shows the final result. You may also want to set the Default Gateway Address and DNS nodes if you are connected to the Internet.
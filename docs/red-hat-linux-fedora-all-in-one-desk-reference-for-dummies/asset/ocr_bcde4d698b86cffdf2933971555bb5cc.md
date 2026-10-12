![](bbox=[0.22, 0.17, 0.6, 0.53])

Figure 3-7:
Activate the new wireless device from this window.

8. Select the new wireless device, and then click the Activate button on the toolbar (refer to Figure 3-7).

A dialog box informs you that the changes have to be saved before activating the wireless device and asks if you want to continue.

9. Click Yes and then OK when another dialog box prompts you to activate the network device.

If all goes well, the wireless network should be up and running after a few moments.

![](bbox=[0.13, 0.7, 0.22, 0.85])

The Network Configuration tool saves your wireless network settings in a text file whose name depends on the wireless network device name. If the wireless network device name is eth0, the configuration is stored in the text file /etc/sysconfig/network-scripts/ifcfg-eth0. If the wireless device name is eth1, the file is /etc/sysconfig/network-scripts/ifcfg-eth1. This configuration file contains various settings for the wireless network card. Table 3-1 explains the meaning of the settings. Here is a slightly edited version of the /etc/sysconfig/network-scripts/ifcfg-eth1 file from my laptop PC:

```
USERCTL=no
PEERDNS=yes
TYPE=Wireless
DEVICE=eth0
HWADDR=00:02:2d:8c:f9:c4
BOOTPROTO=dhcp
ONBOOT=no
DHCP_HOSTNAME=
NAME=
```
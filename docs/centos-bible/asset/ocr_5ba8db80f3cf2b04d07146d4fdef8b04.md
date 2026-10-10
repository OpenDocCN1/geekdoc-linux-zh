# Part IV  Networking

# Activating the Wireless Interfaces

To immediately activate the wireless interface you just configured, select the Wireless entry on the Network Configuration window and click on the Activate button. After a few seconds, the Status should appear as Active.

To have the interface start when you reboot your computer, click on the wireless interface from the Network Configuration window and select Edit. From the Wireless Device Configuration window that appears, click on the box next to “Activate device when computer starts.”

If you want to explicitly enter a Network Name (SSID), click on the Wireless Settings tab on the Wireless Device Configuration window. From there, select Specified, type the network name (any name you choose to match others on your wireless network), and click OK.

Be sure to save your changes on the Network Configuration window by clicking File \> Save.

# Checking Your Wireless Connection

Your wireless LAN interface should be operating at this point. If another wireless computer is available on your wireless network, try communicating with it using the ping command and its IP address (as described in the section, “Can You Reach Another Computer on the LAN?” later in this chapter).

If you are not able to communicate with other wireless nodes or if transmission is slow, you may have more work to do. For example, if you see messages that say “Destination Host Unreachable,” instead of the output shown earlier, refer to the section on “Troubleshooting a Wireless LAN” for help.

# Testing Distances

Although you may be thrilled to have a wireless LAN working between two computers, you will probably want these computers to be located some distance from each other to make the LAN useful. Getting your wireless LAN to work at the desired distances can be quite a challenge. See the section, “Selecting Antennas,” earlier in this chapter for suggestions on selecting and using antennas to configure the type of wireless LAN you are interested in.

# Setting Wireless Extensions

After the wireless module is loaded, you can change wireless extensions using the iwconfig command. The iwconfig command is the command that is actually used to set the options added to the ifcfg configuration script (e.g., for the eth1 interface, the script would be /etc/sysconfig/network-scripts/eth1).

Some of the same options that you set when the module was loaded can be reset using the iwconfig command. The iwconfig command can be useful for testing different settings on an active wireless LAN. The syntax of the iwconfig command is as follows.

```
# iwconfig  interface  parameter  value
```
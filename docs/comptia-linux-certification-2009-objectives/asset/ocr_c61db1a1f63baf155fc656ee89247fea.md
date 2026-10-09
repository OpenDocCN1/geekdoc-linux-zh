+   2. Disable the NIC.
   - Enter `cd /etc/sysconfig/network-scripts` and delete the corresponding `ifcfg-eth{Number}` file in the directory.
   - Or, enter `ifdown eth{Number}`.

![](bbox=[0.1, 0.17, 0.77, 0.24])

# Delete a NIC

To delete any NIC devices, delete the corresponding `ifcfg-eth{Number}` file located in the `/etc/sysconfig/network-scripts/` directory.

![](bbox=[0.03, 0.36, 0.77, 0.42])

# Procedure Reference: Configure a Wireless Network Interface Using the iwconfig Command

To configure a wireless network interface using the `iwconfig` command:

+   1. Log in as root in the CLI.
2. Specify the different parameters for the wireless interface.
   - Enter `iwconfig (device number) essid (ess id | network name)` to set the network name for the wireless device.
   - Enter `iwconfig (device number) nwid (network id | domain id)` to set the network id for the wireless device.
   - Enter `iwconfig (device number) nickname (nickname)` to specify the nickname for the wireless device.
   - Enter `iwconfig (device number) mode {Ad-Hoc|Managed|Master|Repeater|Secondary|Monitor|Auto}` to set the mode of the wireless device.
   - Enter `iwconfig (device number) freq|channel (frequency value | channel number)` to set the frequency or channel for the wireless device.
   - Enter `iwconfig (device number) ap (access point id)|any|off` to set the access point for the wireless device.
   - Enter `iwconfig (device number) rate (bit rate)|auto)` to set the bit-rate for the wireless device.
   - Enter `iwconfig (device number) key (key value)` to set the encryption key for the wireless device.
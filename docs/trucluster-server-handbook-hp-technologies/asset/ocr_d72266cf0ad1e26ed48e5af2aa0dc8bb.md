+   - Select the following menu items from the Main Menu:
+     - CMOS setup
+     - Advanced CMOS setup
+     - Console Selection: Digital UNIX Console (SRM)
+   - Press the F10 key to save your selections.
+   - Power off and then power on the system.

# 4.3.3 Host Bus Adapter Firmware

As of Alpha Firmware update version 6.1, the host bus adapter firmware and the Alpha Firmware are updated at the same time. Included on the list of devices to update is the KGPSA host bus adapter – this is the pga0 device. Just make sure that the firmware is updated for this device.

# 4.3.4 HSZ/HSG RAID Array Controller Firmware

Updating the HSZ/HSG RAID Array Controller firmware should be left to the HP Field Service Engineers. Only those customers who really know what they are doing should attempt this update and only after performing a full backup of any data that may be on the storage subsystem.

The minimum HSZ/HSG firmware revisions to support TruCluster Server are represented in Table 4-3.

To determine the firmware level of your HSZ/HSG controller, use the following command:

```
HSG> show this
Controller:
    HSG80 ZG14100634 Software V86F-8, Hardware E16
...
```

In this example, the HSG80 controller is at the ACS firmware revision V86F-8. The "-8" usually signifies the patch level of the firmware. The same conventions and caveats that apply to the HSG ACS firmware can also be applied to the HSOF firmware of the HSZ family of controllers.

# 4.3.5 Fibre Channel Switch Firmware

Again, as with the HSZ/HSG Raid Array Controller firmware, only HP Field Service Engineers should perform updates to the Fibre Channel Switch Firmware.

# 4.4 Configuring and Verifying the Cluster Interconnect Hardware

Implementing a cluster requires a dedicated Cluster Interconnect in which all cluster members are connected. The cluster interconnect provides the foundation for a virtual private network that allows
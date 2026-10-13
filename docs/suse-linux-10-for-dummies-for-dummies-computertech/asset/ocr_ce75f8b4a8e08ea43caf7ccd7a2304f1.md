![](bbox=[0.231, 0.135, 0.731, 0.445])

**Figure 8-5:** Configuring a new wireless Ethernet card in SUSE Linux.

From the screen shown in Figure 8-5, follow these steps:

+   1. **Click Add (see Figure 8-5).**
+   
+      YaST displays the Manual Network Card Configuration screen. If the card was not correctly detected, click Select from List and select the card from the list that appears. Click Next to continue. YaST displays the Network Address Setup screen. You can click Next to leave this at the default setting of automatic address setup via DHCP (Dynamic Host Configuration Protocol). YaST displays the Wireless Network Card Configuration screen (see Figure 8-6).
+   
+   2. **Enter the needed wireless network card parameters and click OK.**
+   
+      You can leave the Operating Mode as Managed, but you do have to enter certain parameters to enable the wireless network card to communicate with the wireless access point. For example, you have to specify the wireless network name assigned to the access point—and the encryption settings must match those on the access point.

That should get the wireless card ready to go.

![](bbox=[0.13, 0.801, 0.21, 0.873])

To check the status of the wireless network interface, type **su -** to become root and then type the following command:

```
```text
iwconfig
```
```
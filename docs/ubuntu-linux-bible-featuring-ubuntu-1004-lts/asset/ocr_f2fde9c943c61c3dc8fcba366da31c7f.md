wlan0 IEEE 802.11b/g+ SSID:"wvh" Nickname:"acx v0.3.36"
Mode:Managed Frequency:2.437 GHz Access Point: 00:06:25:7B:CE:3F
Bit Rate:5.5 MB/s Tx-Power=15 dBm Sensitivity=1/3
Retry limit:7 RTS thr:off
Power Management:
Link Quality=31/100 Signal level=3/100 Noise level=0/100
Rx invalid uuid:0 Rx invalid crypt:0 Rx invalid frag:0
Tx excessive retries:0 Missed beacon:0

In this case, new wireless device on this system is wlan0, which you should then enter the name of your wireless device in the dialog in Figure 22-5. If you change the name of your (or wireless) device, you can then click Close to close the Preferences dialog, and select the Refresh menu option in the Wcid Manager to re-probe your networked environment and identify the wireless networks that can be detected using the new device.

The other option that I find in the dialog shown in Figure 22-5 is the "Always show wire interface" option, which should be selected to always list your wireless interface in the main Wcid Manager dialog.

To see additional Wcid settings, click the External Tabs to display the pane shown in Figure 22-6. Although you will rarely have to modify any of the settings on this dialog, doing enables you to identify a specific application that you want to use as a DHCP client, to purge the routing table when switching network connections, and to display the password prompt when you attempt privileged operations such as network configuration.

Similarly, the Preference dialog's Advanced Settings tab provides other low-level configuration settings, as shown in Figure 22-7 Although you will rarely have to modify any of the settings on this dialog, you can select another application use to exchange authentication information. If you are using the NDIS Wrapper application (discussed later in this chapter) to use Microsoft Windows network drivers on your Linux system, your system may automatically set the WPA Supplicant application to "ndiswrapper," I usually have to go back to "west" to get working correctly. And occasionally activating debugging when working with a stubborn wireless adapter (which writes detailed information to the Wcid log file in /var/log/wcid/wcid.log) are the only configuration changes that I've ever had to make on this dialog.

After making changes or simply examining Wcid's current configuration, click OK to close the Preferences dialog and return to the Wcid Manager.
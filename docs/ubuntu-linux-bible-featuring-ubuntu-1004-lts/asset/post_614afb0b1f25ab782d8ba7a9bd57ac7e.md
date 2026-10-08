
If you are using a version of Ubuntu other than Linux Lynx (10.04), you should replace lucid with the name of the version of Ubuntu that you are using (karmic, jackalope, hardy, etc.). If you are using Synaptic, it will automatically update the lists of available packages that it knows about. If you directly modified your /etc/apt/sources.list file, you will need to tell whatever management software you are using to update its package lists. If you are using aptitude to install software, you can do this by executing the command `sudo aptitude update` from command-line environment. If you have problems updating package manager list of available packages, see Chapter 19 for more information about updating package lists in whatever package manager you are using.

Before installing Wicd, you should also import its privacy key so that your package manager won't warn you about the dangers of installing software from unauthorized sources. You can import this key from any command-line environment by executing the following command:

```
wget -q http://apt.wicd.net/wicd.gpg 0- | sudo apt-key add
```

After installing Wicd, you can use your favorite package management tool to install the wicd package. As a replacement for the Network Manager and its applets, Wicd conflicts with the Network Manager, and only one of these network connection packages can be installed on a system at a time. However, as mentioned previously, installing Wicd will automatically purge the Network Manager and related applets for you. Installing Wicd will automatically purge the Wicd daemon and install both the Wicd daemon (/usr/bin/wicd) and a Python-based client application for your Ubuntu system's Notification Area. This client application will start automatically the next time that you log in your system, but if it doesn't start automatically when you install Wicd, you can execute it manually by executing the command `/usr/bin/wicd-client&` from any command-line environment.

## Using Wicd

To start the client portion of Wicd, click on its tray icon to display a screen like the one shown in Figure 22-1.

This initial dialog should show an entry for the wired connection on your system and any wireless networks that have been detected. The wireless networks that are listed depend on those that are detected in your location—if the screen that you see when you first start Wicd looks exactly like the one shown in Figure 22-1, then I'm flattered (and a little creeped out) that you're reading this book from somewhere in my.

As you can see Figure 22-1, Wicd initially identifies all available wired and wireless connections, but does not automatically connect to any of them by default. To connect to any of them, click the Connect button below that entry. If you attempt to connect to a network that requires authentication, you will immediately see a dialog like the one shown in Figure 22-2, which tells you that the connection requires encryption.

## Chapter 22: Going Wireless

### FIGURE 22-1
The Wicd Network dialog

![](img/1a233c34336fbf5a85d6eb785e401709_844_0.png)

### FIGURE 22-2
Attempting a connection that requires a password or key

![](img/1a233c34336fbf5a85d6eb785e401709_844_1.png)

## Part II: Ubuntu for Desktop Users

If you see the dialog shown in Figure 22-2, click OK to dismiss it, which automatically displays the dialog that is normally shown by clicking the Properties button below the name of the network that you are attempting to connect to. This dialog contains fields and dropdowns that you must use to define the encryption/authentication information that is required to establish a connection to network, as shown in Figure 22-3.

### FIGURE 22-3
Configuration options for a given wireless network

![](img/1a233c34336fbf5a85d6eb785e401709_845_0.png)

Make sure that "Use Encryption" checkbox is selected, and click the dropdown list near the bottom of this dialog to display your encryption and authentication options. Select the mechanism that is used by the wireless network that you want to connect to, and enter the information it requires in the fields that are displayed. For example, Figure 22-3 shows the area for entering a hexadecimal WEP key for a network that uses WEP.

### Tip
Each wireless network shown in the dialog in Figure 22-1 identifies the type of encryption or authentication that it uses in the heading for wireless network. For example, you can see that the wireless network vwhh does not use authentication or encryption, while the wireless network PY3N3 uses WEP.

After entering the information required by the encryption or authentication mechanism associated with the wireless network that you want to connect to, click OK to close the Properties dialog and return to a screen like the one shown in Figure 22-1. If you want to try to connect to this wireless network each time you start your system, select the "Automatically connect to this network" option. Click Connect to connect to the specified wireless network. You will see status messages and a progress bar at the bottom of the Wdic Manager dialog, and the Wdic Manager will display a screen like the one shown in Figure 22-4 once the connection has been established successfully.

### FIGURE 22-4
A successful connection to a wireless network

![](img/1a233c34336fbf5a85d6eb785e401709_846_0.png)

This dialog displays the IP address and transmission rate for your connection at the bottom of the Wdic Manager. You can now close Wdic Manager by clicking Close in its upper right corner. That's all really is to it, except for some optional Wdic that you may want to do.

## Chapter 22: Going Wireless
If you are using the NDIS Wrapper application (discussed later in this chapter) to use Microsoft Windows network drivers on your Linux system,. Configuring Wicd is discussed in the next section.

## Configuring Wicd ownTo configure Wicd, select the Preferences menu from the Wdic to display, as shown in Figure 22-5.

### Part II: Ubuntu for Desktop Users
Setting preferences for Wicd

![](img/1a233c34336fbf5a85d6eb785e401709_847_0.png)

In most cases, new device on this system is wlan0, which you should then enter the name of your wireless in the dialog in Figure 22-5. If you change the name of your (or wireless) device, you can then click Close to close the Preferences dialog, and select the Refresh menu in the Wdic Manager to re-probe your networked environment and identify the wireless networks that can be detected using the new device.

The other option that I find in the dialog shown in Figure 22-5 is the "Always show wire interface" option, which should be selected to always list your wireless interface in the main Wcid Manager.

To see additional Wcid settings, click the External Tabs to display the pane shown in Figure 22-6. Although you will rarely have to modify any of the settings on this dialog, doing enables you to identify a specific application that you want to use as a DHCP client.

Sample output from this command:
```
$ ifconfig
lo
eth0
irda0
pan0
wlan0
```
```
```:
Rx invalid uuid:0 Rx invalid crypt:0 Rx invalid frag:0
Tx excessive retries:0 Missed beacon:0
```

```
wlan0 IEEE 802.11b/g SSID:"acx" Mode:Managed Frequency:2.437 GHz Access Point: 00:06:25:CE:3F
Bit Rate:5.5 MB/s Tx-Power=15 dBm Sensitivity=1/100
Retry limit:7 RTS:off
Power Management:on
Link Quality=31/100 Signal level=3/100 Noise level=0/100
```

After making changes or simply examining Wcid's current configuration, click OK to close the Preferences dialog and return to the Wcid Manager.

# ### Portable Wi-Fi signal repeater

Boost your signal using a Raspberry Pi and two USB Wi-Fi dongles

What we like about the Raspberry Pi for this project is that it's very low maintenance and extremely easy to put in an appropriate location. All you need for this project are two USB wireless adaptors, a nice little case and a way to power it. Once you've set it up, you can basically leave it to its own devices, checking in over SSH every now and then to do some updates.
Set this up on a monitor with a keyboard, using a fresh image of Raspbian and with your Wi-Fi dongles plugged in. On first boot keep it as CLI and after doing the usual apt-get updates and upgrades,

type startx to get to the desktop. Configure the wireless for wlan0 to connect to your home network and make sure it has a fixed IP address, then reboot to make sure it all works from the command line by using ping www.google.com. Now you need to install your first bit of software using:

```
`$ sudo apt-get install hostapd iw`
```

After it's installed, you'll want to download and save the file we've created directly to config by entering the following two commands:

+   ### What you'll need
+   
+   * 2 USB Wi-Fi adaptors
+   * Raspberry Pi case
+   * Portable power pack

![](bbox=[0.02, 0.43, 0.98, 0.95])

**Right** One Wi-Fi adaptor picks up your main Wi-Fi network, while the other one broadcasts a new signal
# PRINT WIRELESSLY WITH YOUR RASPBERRY PI

![](bbox=[0.11, 0.11, 0.43, 0.27])

# 02 Detect your printer

With your Raspberry Pi set up as usual and the printer connected to a spare USB port, enter:

```
lsusb
```

This will confirm that the printer has been detected by your Raspberry Pi. In most cases you should see the manufacturer and model displayed.

# 03 Install Samba and CUPS

Install Samba to enable file and print sharing across the entire network:

```
sudo apt-get install samba
```

Next, install CUPS:

```
sudo apt-get install cups
```

With a print server created, begin configuration by adding default user 'pi' to the printer admin group:

```
sudo usermod -a -G lpadmin pi
```

# 04 Set up print admin

Set up the CUPS print admin tool first. Boot into the GUI (startx) and launch the browser, entering 127.0.0.1:631. Here, switch to Administration and ensure the 'Share printers' and 'Allow remote administration' boxes are selected. Next, select Add Printer and enter your Raspbian username and password when prompted.

![](bbox=[0.12, 0.65, 0.44, 0.73])

# 05 Add your printer

A list of printers will be displayed, so select yours to proceed to the next screen where you can confirm the details, add a name and check the Share This Printer box. Click Continue to load the list of printer drivers and select the appropriate one from the list.

# 06 Configure Samba for network printing

Using a Windows computer for printing? Samba will need some configuration. Open /etc/samba/smb.conf in nano, search (Ctrl+W) for [printers] and find 'guest ok' which you should change as follows:

```
guest ok = yes
```

Next, search for *[print$]*. Then change the path as follows:

```
path = /usr/share/cups/drivers
```

# Begin configuration by adding the default user 'pi' to the printer admin group

# 07 Join a Windows workgroup

With these additions made, search for 'workgroup' in the configuration file and add your workgroup:

```
workgroup = your_workgroup_name
wins support = yes
```

Make sure you uncomment the second setting so that the print server can be seen from Windows. Save your changes and then restart Samba:

```
sudo /etc/init.d/samba restart
```

![](bbox=[0.47, 0.36, 0.92, 0.56])

# 08 Accessing your printer on Linux

Meanwhile, it's a lot easier to access your wireless printer from a Linux, Mac OS X or other Unix-like system, thanks to CUPS. All you need to do is add a network printer in the usual way and the device will be displayed.

![](bbox=[0.47, 0.66, 0.92, 0.81])

# 09 Add AirPrint compatibility

It's also possible to print wirelessly from your iPad using Apple's AirPrint system. To do this, you need to add the Avahi Discover software:

```
sudo apt-get install avahi-discover
```

Your wireless printer will now be discoverable from your iPad or iPhone and will be ready to print.
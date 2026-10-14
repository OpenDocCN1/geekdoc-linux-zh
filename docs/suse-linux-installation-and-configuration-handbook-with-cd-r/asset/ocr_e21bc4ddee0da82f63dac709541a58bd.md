Luckily, SuSE Linux includes a YaST module that configures WvDial. The next section explains how to configure WvDial manually and by using the YaST module.

# Configuring WvDial Using YaST

You can use YaST to configure a modem connection without having to go through the trouble of editing files and configuring devices. YaST uses interactive menus to set up a connection from the ground up. To set up a connection using YaST, follow these steps:

+   1. Start YaST.
+   2. Open System Administration, Network Configuration, Configure a PPP Network. This will bring up the SuSE WvDial Configuration window (see Figure 23.3).

# FIGURE 23.3
SuSE WvDial Configuration window.

![](bbox=[0.25, 0.48, 0.75, 0.72])

# SuSE WvDial Configuration

The first step in WvDial configuration is to configure it to detect your modem. To do so, highlight the Autodetect Modem option and press Enter. WvDial will attempt to scan your serial ports looking for a modem. After it finds one, WvDial will attempt to communicate with the modem and find the best init and dial strings to use with the modem. Scroll down the output window to check the output of the wvdialconf program.

Next, you must edit the connection profile by highlighting the Configure the Current Profile option and pressing Enter. Once in the Configure the Current Profile menu, fill in the following values (see Figure 23.4):

+   - Phone number—Your ISP phone number.
+   - Area code—The area code of your ISP. You can leave this field empty if you are dialing from the same area.
+   - Account name—The username you use to connect to this ISP.
+   - Password—Your password.
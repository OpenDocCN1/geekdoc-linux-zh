# Chapter 15: Setting Up Your Internet Connection

Figure 15-3:
Using YaST
to make
t link
between
/dev/tty
2 and
/dev/modem.

![](bbox=[0.183, 0.115, 0.658, 0.37])

# Configuring your PPP Network

At this point, you are ready to configure your Linux system to dial up your ISP. You can use the program WvDial to do this. Luckily, YaST has a dialog box for configuring your account information and dialing the modem. The following steps describe how to do this.

+   1. Log into Linux and start the X Window system.
2. Start YaST, which you can do by clicking the yellow icon on the panel at the bottom of your screen.

If you are not logged in as root, you will be prompted for the root password.
3. Select System Administration from the main menu and press Enter.
4. Select Network configuration from the System Administration submenu and press Enter.
5. Select Configure a PPP network from the Network configuration submenu and press Enter.
6. Configure the current profile and press Enter.

You will be presented with the WvDial configuration dialog box. You can use this dialog box to configure your dial-up settings.

This dialog contains a few parameters that you need to set, including your username, your password and the phone number of your ISP. These three settings can easily be configured by highlighting them, pressing Enter, and entering the appropriate information into the text boxes.
hand, but only provide root's password and some information about the ISP or hosting service that you are calling.

Once kudzu, or the Red Hat hardware detection tool has properly detected and configured the modem attached to your machine, you can begin configuring the software under Linux to establish a dial-up connection to your Internet Service Provider. Both steps are very easy since Red Hat takes much of the guesswork out of your hands and does a fine job in installing the proper settings for your machine.

Setting up your modem under Linux is now a simple task. If you are using an external modem, shut down your machine and then plug the connection into an available COM port with a cable supplied by the manufacturer. If you are using an internal modem, verify that the device is not a WinModem, open the case, and insert the card into the proper available slot. Start up Linux again and wait for kudzu to detect your modem. If kudzu does not detect your modem initially during the bootup sequence, you can still configure it using the rp3-config program.

As root under any X Window terminal, enter **rp3-config**. The program presents the screen shown in Figure 16.9.

Next, the rp3-config program checks your system for any existing modems and verifies whether you have already configured a modem under the control panel or the netcfg utility. You will be simply prompted to allow the system to check all devices for any attached modems as shown in Figure 16.10.

![](bbox=[0.1, 0.56, 0.63, 0.93])

# FIGURE 16.9

The splash screen for creating a new Internet connection under the Gnome desktop using the rp3-config command.
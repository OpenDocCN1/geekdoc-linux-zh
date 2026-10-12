
![](img/a0884097af3186d9b4f616aaa3f065b0_600_0.png)

## FIGURE 16.4

Editing the Communication options on the PPP interface.

To place an additional command before the `timeout` variable, you click on the Timeout line and then click Insert. Fill out the values, then click Done. To append a line to the end of the script, press Append, complete the required field, then click Done.

The Networking tab is for setting the interface connection rate, timeout, packet sizes, and so on (see Figure 16.5). You can use this window to specify additional information for the system and to customize the connection.

The final tab under the Edit PPP Interface dialog box is PAP (see Figure 16.6). In the PAP tab, you enter a username and secret password. Much like the step described previously where you insert the login and password variables, here you can accomplish the same thing. This tab enables you to rewrite the contents of the /etc/ppp/pap-secrets file. You can also use this tab to set up chat expressions to test your modem’s connection.

![](img/a0884097af3186d9b4f616aaa3f065b0_600_1.png)

## FIGURE 16.5

Changing the Networking values for a PPP connection.

Once all the correct variables are in place, you may return to the netcfg main window. Then click the Interfaces button to enable the connection (see Figure 16.7). Simply highlight the ppp0 connection and then click the Activate button. Your modem should dial, connect, and shake hands with the ISP’s modem. After a few moments, you will be able to test your connection by attempting a ping or telnet command to contact a location remote from your network.

![](img/a0884097af3186d9b4f616aaa3f065b0_601_0.png)

## FIGURE 16.6

Configuring the PAP-secrets file under netcfg.

Once you click the Activate button, the Network Configurator script will dial in to your Internet provider and begin executing the script you entered previously. With many of the PPP dial-in scripts provided, you will see a Debug button somewhere on the screen. This will assist in tracking down any errors you may encounter when attempting to dial into another provider.

### Enabling a Dial-Up Connection under linuxconf

Setting up a similar connection under the linuxconf program can be just as simple and will also dial up and connect to the ISP. As shown in Figure 16.8, linuxconf’s routine is very similar to that of netcfg. The same windows are present along with the same fields. Here also you may activate the connection and edit the variables.

In both the netcfg and linuxconf windows, you can configure your machine so that it will activate the connection upon bootup. This allows you to connect immediately to the ISP as your machine comes on. Depending upon the fair use procedures defined by your ISP, you can remain online for as long as the ISP allows.

Under the very latest release of Red Hat Linux, the PPP/SLIP configuration interface is not available. It is recommended that users wishing to create a dial-up connection to an Internet Service Provider use the Red Hat PPP Dialer, which can be executed from the command line by typing the executable rp3. This replaces the linuxconf PPP dial-up utility.

### Using GNOME and KDE Dial-Up Utilities

One of the easiest methods of creating a dial-up connection is to use a tool such as the GNOME rp3-config and rp3 utility and the KDE kppp program. Both are available with the latest Red Hat release. If you wish to use the KDE kppp program, you must choose to install the KDE programs during the initial Red Hat Linux installation or install them at a later time. Both the KDE dialup tool and the GNOME rp3 program can be used under different window managers. They are not dependent upon their respective window manager or environment in order to run. In other words, you do not have to be running the KDE desktop environment in order to use kppp.

Both rp3 and kppp offer many unique features that make the tools even more versatile than that of the netcfg and linuxconf configuration programs:

- They require just one window to connect.
- They prompt for a root password rather than forcing you to change the permission of the binary itself.
- They monitor your connections and show modem activity.
- They measure the bandwidth usage in an easy-to-read graph form.
- They can calculate phone costs based on connection time or transfer of bytes.
- They can dock into the Gnome or KDE toolbar.
- You can set up multiple connections to other ISPs.

You can start either utility at the command line by typing its respective filename. You should run each program as root. Otherwise, the program will prompt you for the root password.

### Setting Up the rp3 Utility under Gnome

A major step in assisting the novice user with Linux is the GNOME desktop's Dialup Connection Wizard. Similar to the wizards used under the Windows operating system, this tool detects your attached modem, sets up the variables, and then provides easy connectivity. You are not required to edit any files by hand, but only provide root's password and some information about the ISP or hosting service that you are calling.

Once kudzu, or the Red Hat hardware detection tool has properly detected and configured the modem attached to your machine, you can begin configuring the software under Linux to establish a dial-up connection to your Internet Service Provider. Both steps are very easy since Red Hat takes much of the guesswork out of your hands and does a fine job in installing the proper settings for your machine.

Setting up your modem under Linux is now a simple task. If you are using an external modem, shut down your machine and then plug the connection into an available COM port with a cable supplied by the manufacturer. If you are using an internal modem, verify that the device is not a WinModem, open the case, and insert the card into the proper available slot. Start up Linux again and wait for kudzu to detect your modem. If kudzu does not detect your modem initially during the bootup sequence, you can still configure it using the rp3-config program.

As root under any X Window terminal, enter **rp3-config**. The program presents the screen shown in Figure 16.9.

Next, the rp3-config program checks your system for any existing modems and verifies whether you have already configured a modem under the control panel or the netcfg utility. You will be simply prompted to allow the system to check all devices for any attached modems as shown in Figure 16.10.

![](img/a0884097af3186d9b4f616aaa3f065b0_604_0.png)

## FIGURE 16.9

The splash screen for creating a new Internet connection under the Gnome desktop using the rp3-config command.

![](img/a0884097af3186d9b4f616aaa3f065b0_605_0.png)

## FIGURE 16.10

Allow the system to select your modem.

The rp3-config utility now checks through all available /dev/ttyS devices and listens for a dial tone. If kudzu did not detect a modem during the bootup sequence or after running kudzu manually, the program prompts you to allow the rp3-config program to detect the modem now. Turn your modem on and make certain that the analog line phone cord is plugged in the correct port on the modem itself. The rp3 utility then checks for an operational modem and tests for a dial tone. As shown in Figure 16.11, it functions much like a Windows Wizard and looks through your system for the proper hardware and then configures it appropriately.

![](img/a0884097af3186d9b4f616aaa3f065b0_605_1.png)

## FIGURE 16.11

The rp3-config command examines all ports and devices for any connected modems.

If you do not already have a modem set up under your Linux settings, the screen shown in Figure 16.12 appears. Here you can enter the settings for your modem manually. This screen often appears if you do not have an active phone line plugged into your machine.

If the program detects no modems on your system, you may still enter the settings manually. If the program detects a modem, a window similar to that shown in Figure 16.11 appears, in which you may either confirm the detected setting, modify the settings, or add an additional modem.

Next the program prompts you to create an account name for this particular account. Hit the Next button and you will be shown a dialog box much like the one in Figure 16.13. You should stay with the same format as used by Linux. If you have a single modem, name the account **ppp0**. This name will create less confusion later if you decide to alter the settings yourself. However, if you wish to identify your connection by a less cryptic name, you may name the connection whatever you wish. Most users choose the name of the ISP to whom they are connecting.

If the phone from which you are dialing requires a prefix to reach a dial tone, such as a 9 or pound sign (#), enter that number or character in the Prefix field. If you are dialing from a home computer or you do not require an escape character, leave this field empty. Now enter the area code and phone number of your ISP. As the screen in Figure 16.13 shows, the prefix and area-code are optional.

![](img/a0884097af3186d9b4f616aaa3f065b0_606_0.png)

## FIGURE 16.12

Entering the manual settings for your modem.

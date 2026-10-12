which can be executed from the command line by typing the executable rp3. This replaces the linuxconf PPP dial-up utility.

# Using GNOME and KDE Dial-Up Utilities

One of the easiest methods of creating a dial-up connection is to use a tool such as the GNOME rp3-config and rp3 utility and the KDE kppp program. Both are available with the latest Red Hat release. If you wish to use the KDE kppp program, you must choose to install the KDE programs during the initial Red Hat Linux installation or install them at a later time. Both the KDE dialup tool and the GNOME rp3 program can be used under different window managers. They are not dependant upon their respective window manager or environment in order to run. In other words, you do not have to be running the KDE desktop environment in order to use kppp.

Both rp3 and kppp offer many unique features that make the tools even more versatile than that of the netcfg and linuxconf configuration programs:

+   - They require just one window to connect.
+   - They prompt for a root password rather than forcing you to change the permission of the binary itself.
+   - They monitor your connections and show modem activity.
+   - They measure the bandwidth usage in an easy-to-read graph form.
+   - They can calculate phone costs based on connection time or transfer of bytes.
+   - They can dock into the Gnome or KDE toolbar.
+   - You can set up multiple connections to other ISPs.

You can start either utility at the command line by typing its respective filename. You should run each program as root. Otherwise, the program will prompt you for the root password.

# Setting Up the rp3 Utility under Gnome

A major step in assisting the novice user with Linux is the GNOME desktop's Dialup Connection Wizard. Similar to the wizards used under the Windows operating system, this tool detects your attached modem, sets up the variables, and then provides easy connectivity. You are not required to edit any files by
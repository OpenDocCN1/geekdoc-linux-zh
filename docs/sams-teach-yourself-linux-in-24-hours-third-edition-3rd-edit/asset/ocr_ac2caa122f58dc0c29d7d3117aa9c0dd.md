![](bbox=[0.2, 0.18, 0.27, 0.3])

> Many Linux distribution vendors have created their own configuration utilities for the /etc/X11/XF86Config file: Red Hat has XConfiguror, SUSE has SAX, Mandrake has XFDrake, and TurboLinux has turbocfg, to name a few. All these vendor-supplied programs should work to varying degrees to get you through the configuration of your X server. However, since the arrival of X11R6 release 4.0, many of these distribution specific utilities don't function as well anymore and need updating. But, as luck would have it, the X.org people already have an updated utility, xf86config, that is present in all Linux distributions so that's the one we will concentrate on in this hour.

# Task: Configuring X11 with the xf86config Command

To begin configuring the X Window System to fine-tune your video display, you will need to be logged in to the root account. As you step through each process, you might want to keep your Linux diary next to you and write down the steps you performed during the configuration. To begin working with xf86config, perform these steps at the command line:

+   1. Start the configuration process. Type xf86config and press Enter. The opening screen appears. Read the information and press Enter to move to the next screen.
+   2. Select your mouse. Several mouse types (as shown in Figure 18.3) are listed. Type the number that applies to the mouse that is attached to your computer and press Enter. If you use a two-button mouse, you will be asked whether you want the mouse to act like a three-button mouse. Type y and press Enter.
+   3. Select a mouse device. Press Enter to select the default device of /dev/mouse.
+   4. Elect to use Xkeyboard extension. Type y and press Enter.
+   5. Select a keymap (the type of keyboard that is attached to the computer). Press Enter to display the list of keyboards. Type the number that corresponds to your keyboard and press Enter.
+   6. Set monitor specifications. Press Enter to display the list of available monitor types (shown in Figure 18.4). Type the number that most closely matches the specifications for your monitor and press Enter.
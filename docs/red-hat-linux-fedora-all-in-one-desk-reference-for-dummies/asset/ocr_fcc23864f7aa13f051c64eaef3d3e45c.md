around the firstboot process and configure X again before you can continue the normal course of events that Red Hat has planned for you. Here's what you should do:

+   1. **Press Ctrl+Alt+F1 to get back to the boot screen.**
+      You see the text display with the boot messages that stop at a line displaying information about firstboot.
+   2. **Press Ctrl+Alt+Del to reboot the PC.**
+      The PC starts to boot and you get to a screen where the GRUB boot loader prompts you and press Enter to boot Red Hat Linux.
+   3. **Press A to add an option for use by the Linux kernel.**
+      The GRUB boot loader then displays a command line for the Linux kernel and prompts you to add what you want.
+   4. **Type a space followed by the word single and then press Enter.**
+      The Linux kernel boots in a single-user mode and displays a prompt that looks like the following:
+      ```
+      sh-2.05b#
+      ```
+      Now you're ready to configure X.

X uses a configuration file, called XF86Config, to figure out the type of display card, monitor, and the kind of screen resolution you want. The Red Hat installer prepares the configuration file, but sometimes the configuration isn't correct.

To quickly create a working XF86Config file, follow these steps:

+   1. **Type the following command:**
+      ```
+      /usr/X11R6/bin/XFree86 -configure
+      ```
+      The screen goes blank and then XFree86 exits after displaying some messages. The last line of the message says the following:
+      ```
+      To test the server, run 'XFree86 -xf86config //XF86Config.new'
+      ```
+   2. **Try the new configuration file by typing the following command:**
+      ```
+      /usr/X11R6/bin/XFree86 -xf86config //XF86Config.new
+      ```
+      If you see a blank screen with a X-shaped cursor, the configuration file is probably working fine.
+   3. **Press Ctrl+Alt+Backspace to kill the X server.**
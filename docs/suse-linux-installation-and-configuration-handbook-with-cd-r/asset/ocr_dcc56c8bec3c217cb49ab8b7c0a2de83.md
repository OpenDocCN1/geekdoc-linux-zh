+   1. Log in as root.
+   2. Change the directory to the Linux kernel sources directory:
+      `#cd /usr/src/linux`
+   3. Start the kernel's configuration modules by typing the following:
+      `#make menuconfig`
+   4. The kernel configuration module will start; navigate to Character Devices, Joysticks and press Enter.
+   5. Highlight Joystick Support and press Y to include it in your kernel.
+   6. Highlight your joystick type from the list and press Y to include it in your kernel.
+   7. Press Esc twice to exit the Joysticks menu.
+   8. Press Esc twice to exit the Character Devices menu.
+   9. Press Esc twice again to exit the kernel configuration module. It will ask you whether you want to save your new kernel configuration; choose Yes.
+   10. Now you need to recompile your kernel for these changes to take effect. To do so, type in the following commands, one after the other:
+       `#make dep`
+       `#make clean`
+       `#make bzImage`
+       `#make modules`
+       `#make modules_install`
+   11. Each of these commands will take some time to execute, and a lot of text will scroll by—don't worry, this is normal. When all the commands have executed, reboot your system.

When the system reboots, your joystick should be detected as /dev/js0. Instruct any games you have to use this device file to access your joystick.

# Fax

Even though email has proven to be a faster and cheaper method of exchanging messages and documents, people still use fax machines. You can use your SuSE Linux box to send and receive faxes if you have a fax-modem installed. SuSE Linux has a fax package called HylaFax. This is a powerful faxing server that turns your Linux box into a fax server on the network.

Configuring HylaFax can be quite complicated. However, configuring it for personal use is not that hard. First, you will need to install the packages.

Package requirements:

Series d:

+   - javarunt
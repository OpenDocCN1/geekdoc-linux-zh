+   3.  **If you have any SCSI device, such as a SCSI hard drive, select SCSI and press Enter.**
+       The installer displays a list of SCSI controllers. When you select the one on your system and press Enter, the installer then loads the appropriate driver module. The SCSI driver automatically probes and determines the SCSI controller's settings.
+       After you add any SCSI controllers, you're back at the initial dialog box — and from there you can add network cards.

+   4.  **If you select Network from the list and press Enter, the installation program displays a list of network cards from which you can select your network card.**
+       When you press Enter, the installation program loads the driver module for the selected network card. That driver then probes and determines the network card settings.

+   5.  **[Optional] If you need a Linux device driver that does not come with Fedora Core, try checking the vendor's Web site or a search engine (such as Google — www.google.com).**
+       Many hardware vendors provide Linux device drivers for download, just as they do Windows drivers.
+       After you finish adding the SCSI controllers and network cards, the installer switches to graphics mode and guides you through the rest of the installation.

![](bbox=[0.12, 0.48, 0.19, 0.53])

# ## Troubleshooting X

I have this problem on an older PC every time I install Fedora Core: During installation, the GII installation works fine — but when I reboot the PC for the first time after installation, the graphical login screen does not appear. Instead, the boot process seems to hang just as it starts `firstboot`. If this problem happens to you, here's how you can troubleshoot the problem.

That `firstboot` process happens to be a special step where, if all went well, the Red Hat Setup agent starts and enables you to perform one-time setups (such as date and time configuration) and install programs from any other CDs. The reason `firstboot` may get stuck is because the graphical X environment isn't working on your system. You have to get around the `firstboot` process and configure X again before you can continue. Here's what you do:

+   1.  **Press Ctrl+Alt+F1 to get back to the boot screen.**
+       You see the text display with the boot messages that stop at a line displaying information about `firstboot`.

Book 1
Chapter 3
Troubleshooting and Configuring
Fedora Core
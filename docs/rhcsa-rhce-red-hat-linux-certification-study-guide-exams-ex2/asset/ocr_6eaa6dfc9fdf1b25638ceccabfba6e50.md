administrators appreciate the convenience of multiple open command line consoles, side by side. To that end, I selected the following package groups during the installation process.

+   - Desktops – Desktop Includes the basic GNOME Desktop Environment.
+   - Desktops – Fonts Installs fonts that improve system readability in the GUI.
+   - Desktops – X Window System Adds the server packages associated with the GUI.
+   - Applications – Internet Browser Includes the Firefox Web browser.

The package groups fall into different categories; for example, to select the X Window System package group, I first highlighted the Desktops category in the left-hand pane. I could then select the X Window System package group in the right-hand pane.

In addition, for the physical host system configured for KVM-based VMs, I made sure the Virtualization package groups were included. They should be automatically included if you selected the Virtual Host system category earlier in the installation process.

Once desired packages are selected, click Next. Anaconda then proceeds to the installation process. When the process is complete, you'll see a final screen that confirms the installation, along with an option to reboot the system.

On the system used to write this book, I also installed the OpenOffice.org suite and The GIMP (The GNU Image Manipulation Program).

# On Reboot

When installation is complete, you'll see a final message to that effect, with an option to reboot the system. If you've installed RHEL 6 on a physical system, don't forget to eject or remove the boot disk and/or the installation DVD.

For RHEL 6 installed in a KVM-based VM, you'll need to change the boot device. If it isn't already open, click Applications | System Tools | Virtual Machine Manager. Enter the root administrative password if prompted, and double-click on the desired VM. Then change the boot device with the following steps:

+   1. In the window associated with the VM, click View | Details.
+   2. In the window that appears, shown in Figure 1-16, click Boot Options.
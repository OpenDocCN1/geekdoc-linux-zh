+   - A PnP-compatible device
+   - A PnP-compatible operating system
+   - Most motherboards include many integrated devices on board.
+   - Integrated peripherals can be enabled or disabled quite easily using the CMOS Setup program in the BIOS.
+   - You may need to manage systems that don't have any external peripherals, including a keyboard.
+   - You have a couple of options for managing these types of systems:
+       - SSH
+       - VNC
+   - Drivers are small programs that are loaded into RAM that enable the CPU to communicate with a particular hardware component.
+   - For basic system components, driver software is stored in the BIOS.
+   - Other components require that a driver that is stored on the hard disk be loaded into RAM.
+   - On Linux, drivers can be loaded in two ways:
+       - Loaded as kernel modules after the operating system has started
+       - Compiled directly into the kernel itself
+   - You can view information about your system hardware within the /proc directory.
+   - You can use the following command-line tools to view information about the hardware in your system:
+       - hdparm -a /dev/device
+       - sg_scan
+       - ssciinfo -l
+       - pnpdump
+       - lsusb
+   - You can use the following command-line utilities to manage kernel modules:
+       - `lsmod`    Views loaded kernel modules
+       - `modinfo`    Views module information
+       - `depmod`    Builds a module dependency list
+       - `insmod`    Installs a kernel module but doesn't factor in module dependencies
+       - `modprobe`    Installs or removes a kernel module while taking module dependencies into account
+       - `rmmod`    Removes a kernel module
+   - modprobe uses the /etc/modprobe.conf file to determine which kernel modules should be loaded at boot.
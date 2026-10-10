# 101 System Architecture

# 101.1 Determine and Configure hardware settings

+   - Enable and disable integrated peripherals
+   - Configure systems with or without external peripherals such as keyboards
+   - Differentiate between the various types of mass storage devices
+   - Set the correct hardware ID for different devices, especially the boot device
+   - Know the differences between coldplug and hotplug devices
+   - Determine hardware resources for devices
+   - Tools and utilities to list various hardware information (e.g. lusb, lspeci, etc.)
+   - Tools and utilities to manipulate USB devices
+   - Conceptual understanding of syfs, udev, hald, dbus
+   - The following is a partial list of the used files, terms, and utilities:

+   - /sys
+   - /proc
+   - /dev
+   - modprobe
+   - lsmod
+   - lspeci
+   - lusb

# 101.2 Boot the System

+   - Provide common commands to the boot loader and options to the kernel at boot time
+   - Demonstrate knowledge of the boot sequence from BIOS to boot completion
+   - Check boot events in the log file
+   - The following is a partial list of the used files, terms and utilities:

+   - /var/log/messages
+   - dmesg
+   - BIOS
+   - bootloader
+   - kernel
+   - init
# Introduction

+   - Tools and utilities to list various hardware information (e.g., lusb, lspci, etc.)
- Tools and utilities to manipulate USB devices
- Conceptual understanding of sysfs, udev, hald, dbus
- The following is a partial list of the used files, terms and utilities: /sys, /proc, /dev, modprobe, lmod, lspci, lusb

#  101.2 Boot the System (Chapter 5)

+   - Provide commands to the boot loader and options to the kernel at boot time
- Demonstrate knowledge of the boot sequence from BIOS to boot completion
- Check boot events in the log file
- The following is a partial list of the used files, terms and utilities: /var/log/messages, dmesg, BIOS, bootloader, kernel, init

# 101.3 Change runlevels and shutdown or reboot system (Chapter 5)

+   - Set the default run level
- Change between run levels including single user mode
- Shutdown and reboot from the command line
- Alert users before switching run levels or other major system events
- Properly terminate processes
- Knowledge of basic features of systemd and Uptart
- The following is a partial list of the used files, terms and utilities: /etc/initab, shutdown, init, /etc/init.d, telinit

# 102 Linux Installation and Package Management

# 102.1 Design hard disk layout (Chapter 3)

+   - Allocateys and swap space to separate partitions or disks
- Tailor the design to the intended use of the system
- Ensure the /boot partition conforms to the hardware architecture requirements for booting
- Knowledge of basic features of LVM
- The following is a partial list of the used files, terms and utilities: / (root) filesystem, /var filesystem, /home filesystem, swap space, mount points, partitions
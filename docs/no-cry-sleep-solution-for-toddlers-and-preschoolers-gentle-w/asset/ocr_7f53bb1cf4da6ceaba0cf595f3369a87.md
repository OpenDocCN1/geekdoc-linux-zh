The preceding entry assumes that the Ethernet card was of the same model. If you had added a different model Ethernet card, you would have to specify the module used for that kind of card. In the following example, the second card is a standard PCI Realtek card. Kmod has already automatically detected the new card and loaded the ne2k-pci module for you. You only need to identify this as the eth1 card in the /etc/modules.conf file.

```
alias eth0 3c59x
alias eth1 ne2k-pci
```

A sample modules.conf file is shown here. Notice the aliases for the USB controller and the sound card.

```
alias eth0 3c59x
alias eth1 ne2k-pci
alias parport_lowlevel parport_pc
alias usb-controller usb-uhci
alias sound-slot-0 1810_audio
```

> Tip In some cases, Kmod may not detect a device in the way you want, and thereby not load the kernel module you would like. This was the case in Chapter 30, where you needed to provide SCSI emulation for IDE CD write devices. In this case, kernel parameters were specified to the GRUB boot loader to load the correct modules.

# Installing New Modules for the Kernel

The source code for your Linux kernel contains an extensive set of modules, of which only a few are actually used on your system. When you install a new device, you may have to install the kernel module that provides the drivers for it. This involves selecting the module you need from a list, and then regenerating your kernel modules with the new module included. Then the new module is copied into the module library, installing it on your system. You can then enter it in the /etc/modules.conf file with any options, or use modprobe to install it manually.

First, make sure you have installed the kernel source code in the /usr/src/linux directory (see Chapter 33). If not, simply use an installation utility such as rpm tool or redhat-config-packages to install the kernel source RPM packages. If you are using the source code version of the kernel, unpack it and move its contents to the /usr/src directory.
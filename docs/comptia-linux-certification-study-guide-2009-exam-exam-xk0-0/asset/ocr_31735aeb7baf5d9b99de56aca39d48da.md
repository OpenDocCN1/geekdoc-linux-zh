# ## DEVICE MANAGEMENT

The management of devices on a Linux system is critical, and at first glance can seem more complicated for users of Microsoft Windows getting to grips with Linux. There is often more than one way of managing a device, and often the command line can be used as well as one of many graphical user interfaces (GUIs). The following section will list some of the common commands and major directories that will likely be used on a day-to-day basis by a system administrator.

# ### *lsub*

*lsub* will list all the usb buses on a system and display information about any devices attached to them. The *-v* and *-vv* options will give a verbose output; however, this will only be required during debugging as the output really is verbose, with the *-vv* option giving out all the information the peripheral component interconnect (PCI) device can display. This command is useful to see what usb devices are working and the type of device that is attached.

```
```bash
$ lsub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 005: ID 0204:6025 Chipsbank Microelectronics Co., Ltd
CBM2080 Flash drive controller
Bus 001 Device 003: ID 046d:c517 Logitech, Inc. LX710 Cordless Desktop
Laser
Bus 001 Device 002: ID 413c:0058 Dell Computer Corp. Port Replicator
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
```

# ### *lspci*

The *lspci* command is similar to the *lsub* command, except that it displays all the information regarding the PCI buses in the system and all the devices that are attached to it. This command is useful to understand what devices are attached to the system and the actual driver that should be loaded for the devices. This command can also be used with the *-x* option to display the initial 64 bytes of PCI configuration, which can be useful to see what is loaded.

```
```bash
$ lspci -x
00:00.0 Host bridge: Intel Corporation 82855PM Processor to I/O Controller (rev 03)
```
```
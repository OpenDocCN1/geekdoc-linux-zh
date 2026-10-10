
If you prefer to use a command-line interface, you can use `make menuconfig` to configure the Linux kernel. `menuconfig` provides a graphical wrapper around a text interface. Although it is not as raw as `make config`, `menuconfig` is not a fancy graphical interface either; you cannot use a mouse, but must navigate through it using keyboard commands. The same information presented in `make config` is presented by `make menuconfig`, but as you can see in Figure 36.2, it looks a little nicer. Now, at least, you can move back and forth in the selection process in case you change your mind or have made a mistake.

![](img/34e72348d53ca54c2a1d9c871316691b_831_0.png)

FIGURE 36.2 The make menuconfig utility, a small improvement over make config.

In `make menuconfig`, you use the arrow keys to move the selector up and down and the spacebar to toggle a selection. The Tab key moves the focus at the bottom of the screen to Select, Exit, or Help.

If a graphical desktop is not available, `menuconfig` is the best you can do. However, both `menuconfig` and `xconfig` (see later discussion) offer an improvement over editing the .config file directly. If you want to configure the kernel through a true graphical interface—with mouse support and clickable buttons—`make xconfig` is the best configuration utility option. To use this utility, you must have the X Window System running. The application xconfig is really nothing but a Tcl/Tk graphics widget set providing borders, menus, dialog boxes, and the like. Its interface is used to wrap around data files that are parsed at execution time. Figure 36.3 shows the main menu of xconfig for the 2.6.7 kernel.

After loading this utility, you use it by clicking on each of the buttons that list the configuration options. Each button you click opens another window that has the detail configuration options for that subsection. Three buttons are at the bottom of each window: Main Menu, Next, and Prev(ious). Clicking the Main Menu button closes the current window and displays the main window. Clicking Next takes you to the next configuration section. When configuring a kernel from scratch, click the button labeled Code Maturity Level Options, and then continue to click the Next button in each subsection window to proceed through all the kernel configuration choices. When you have selected all options, the main menu is again displayed. The buttons on the lower right of the main menu are for saving and loading configurations. Their functions are self-explanatory. If you just want to have a look, go exploring! Nothing will be changed if you elect not to save it.

![](img/34e72348d53ca54c2a1d9c871316691b_832_0.png)

FIGURE 36.3 The much nicer make xconfig GUI interface. We recommend that you use this interface if you are able.

If you are upgrading kernels from a previous release, it is not necessary to go through the entire configuration from scratch. Instead, you can use the `make oldconfig` directive; it uses the same text interface that `make config` uses, and it is noninteractive. It just prompts for changes for any new code.

## Using xconfig to Configure the Kernel

For simplicity's sake, during this brisk walkthrough, we assume that you are using `make xconfig`. Prior to this point, we also assume that you have completed the first five steps in the kernel compilation checklist shown previously.

As you learned in the preceding section, you configure the kernel using `make xconfig` by making choices in several configuration subsection windows. Each subsection window contains specific kernel options. With hundreds of choices, the kernel is daunting to configure. We cannot really offer you detailed descriptions of which options to choose because your configuration will not match our own system and setup. Table 36.1 provides a brief description of each subsection's options so that you can get an idea of what you might encounter. We recommend that you copy their kernel's `.config` file to `/usr/src/kernels/2.6` and run make `xconfig` from there. Explore all the options. As long as you do not save the file, absolutely nothing will be changed on your system.

### TABLE 36.1 Kernel Subsections for Configuration

| Name | Description |
|---|---|
| Code maturity level options | Enables development code to be compiled into the kernel even if it has been marked as obsolete or as testing code only. This option should only be used by kernel developers or testers because of the possible unusable state of the code during development. |
| General setup | Contains several different options covering how the kernel talks to the BIOS, whether it should support PCI or PCCMIA, whether it should use APM or ACPI, and what kind of Linux binary formats will be supported. Contains several options for supporting kernel structures necessary to run binaries compiled for other systems directly without recompiling the program. |
| Loadable module support | Determines whether the kernel enables drivers and other nonessential code to be compiled as loadable modules that can be loaded and unloaded at runtime. This option keeps the basic kernel small so that it can run and respond more quickly; in that regard, choosing this option is generally a good idea. |
| Processor type and features | Several options dealing with the architecture that will be running the kernel. |
| Power management options | Options dealing with ACPI and APM power management features. |
| Bus options | Configuration options for the PCMCIA bus found in laptops and PCI hotplug devices. |
| Memory Technology Devices (MTDs) | Options for supporting flash memory devices, such as EEPROMS. Generally, these devices are used in embedded systems. |
| Parallel port support | Several options for configuring how the kernel will support parallel port communications. |
| Plug-and-play configuration | Options for supporting Plug and Play PCI, ISA, and plug-and-play BIOS support. Generally, it is a good idea to support plug-and-play for PCI and ISA devices. |
| Block devices | Section dealing with devices that communicate with the kernel in blocks of characters instead of streams. This includes IDE and ATAPI devices connected via parallel ports, as well as enabling network devices to communicate as block devices. |
| ATA/IDE/MFM/RLL support | Large collection of options to configure the kernel to communicate using different types of data communication protocols to talk to mass storage devices, such as hard drives. Note that this section does not cover SCSI. |
| SCSI device support | Options for configuring the kernel to support Small Computer Systems Interface. This subsection covers drivers for specific cards, chipsets, and tunable parameters for the SCSI protocol. |
| Old CD-ROM drivers | Configuration options to support obscure, older CD-ROM devices that do not conform to the SCSI or IDE standards. These are typically older CD-ROM drivers that are usually a proprietary type of SCSI (not SCSI, not IDE). |
| Multi-device support | Options for enabling the kernel to support RAID devices in (RAID and LVM) software emulation and the different levels of RAID. Also contains options for support of a logical volume manager. |
| Fusion MPT device support | Configures support for LSI’s Logic Fusion Message Passing Technology. This technology is for high-performance SCSI and local area network interfaces. |
| IEEE1394 (firewire) support | Experimental support for FireWire devices. |
| I2O device support | Options for supporting the Intelligent Input/Output architecture. This architecture enables the hardware driver to be split from the operating system driver, thus enabling a multitude of hardware devices to be compatible with an operating system in one implementation. |
| Networking support | Several options for the configuration of networking in the kernel. The options are for the types of supported protocols and configurable options of those protocols. |
| Amateur radio support | Options for configuring support of devices that support the AX25 protocol. |
| IrDA (infrared) support | Options for configuring support of the Infrared Data Association suite of protocols and devices that use these protocols. |
| Bluetooth support | Support for the Bluetooth wireless protocol. Includes options to support the Bluetooth protocols and hardware devices. |
| ISDN subsystem | Options to support Integrated Services Digital Networks protocols and devices. ISDN is a method of connection to a large area network digitally over conditioned telephone lines, largely found to connect users to ISPs. |
| Telephony support | Support for devices that enable the use of regular telephone lines to support VOIP applications. This section does not handle the configuration of modems. |

## Compiling the Kernel

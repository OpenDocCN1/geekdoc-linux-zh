processor from the host machine. It also does not matter whether you have installed your virtual machine on a Windows or a Linux host; you can transfer it between these two supported host operating systems.

Every virtual machine has these hardware specifications:

+   - Same processor as on the host computer
+   - Intel 440BX-based motherboard with NS338 SIO chip and 82093AA IOAPIC
+   - PhoenixBIOS™ 4.0 Release 6 with VESA BIOS
+   - A maximum of 3.6 GB of RAM for each individual virtual machine (with a limit of 4 GB maximum for all virtual machines).
+   - VGA adapter that supports SVGA
+   - A maximum of seven SCSI devices
+   - SCSI controller: Mylex® (BusLogic) BT-958 compatible host bus adapter or an LSI Logic Ultra320 LSI53C10xx SCSI controller)
+   - Virtual SCSI disks with a maximum size of 950 GB
+   - A primary and secondary IDE channel for up to four devices
+   - Virtual IDE disks with a maximum size of 950 GB
+   - A maximum of three AMD PCnet-PCI II compatible Ethernet adapters
+   - Creative Labs Sound Blaster® AudioPCI emulation
+   - Virtual floppy drives (maximum of two), parallel and serial ports, and two USB ports
+   - Two-port USB 1.1 UHCI controller
+   - Keyboard and PS/2 mouse

# 2.9 Creating your First Virtual Machine

It is now time to create your first virtual machine. I will walk you through the steps in the Wizard and will explain all your options. I will also explain what the implications are when selecting settings other than the default.

You create your virtual machine after starting VMware Workstation by selecting New Virtual Machine from the File menu or from the main window. This will start the New Virtual Machine Wizard.

+   1. The first option that you have to select is whether to use the typical or the Custom configuration. I am assuming that you are the investigative type or an advanced user, so we will use the Custom configuration and go through it step by step.
+   2. The next window will be new to users that have worked with version 4.x. You are prompted with the choice (Figure 2.5) to either create a new virtual machine or a legacy machine that is compatible with version 4.
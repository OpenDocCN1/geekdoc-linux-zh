
Switching between bridged networking and host-only networking can be done on-line, when your virtual machines are up and running.

You can either select VM → Settings from the menu and then configure the networking option, or you can double click the network adapter icon on the right lower corner of your virtual machine. This will also bring up the networking control panel.

If you need advanced configuration options and tips on networking, go to section 11: “Networking configurations”

![](img/25fe75b93b97a021effaba85db112a52_36_0.png)

Figure 2.4: The networking configuration can be modified when a machine is on-line.

Tip: I have met a lot of people who have problems with accessing virtual machines and the LAN when they start configuring their physical and virtual adapters. It is very important to make sure that all adapters (physical, including wireless, host-only VMnet1 and VMnet8) are in different IP subnets. A real PC with two network adapters on different Ethernet segments, but with the same IP subnet used on both LANs will not know where to send its packets.

Compare it to a junction with two signs pointing to Paris. You would also be confused as to what direction to choose (unless they both point to Rome, of course, since we know that all roads lead to Rome!).

A PC with a physical adapter and one or more virtual adapters that have been configured for the same subnet will have the same problem and will prevent you from accessing hosts on either the physical or virtual networks.

## 2.8 Virtual Machine Hardware Specifications

A great advantage of virtual machines is that they always provide you with the same hardware. Independent of the hardware in the host system, the hardware inside the virtual machine stays the same. The only component that will be different is the processor, since the virtual machine will work with the underlying processor from the host machine. It also does not matter whether you have installed your virtual machine on a Windows or a Linux host; you can transfer it between these two supported host operating systems.

Every virtual machine has these hardware specifications:

- Same processor as on the host computer
- Intel 440BX-based motherboard with NS838 SIO chip and 82093AA IOAPIC
- PhoenixBIOS™ 4.0 Release 6 with VESA BIOS
- A maximum of 3.6 GB of RAM for each individual virtual machine (with a limit of 4 GB maximum for all virtual machines).
- VGA adapter that supports SVGA
- A maximum of seven SCSI devices
- SCSI controller: Mylex® (BusLogic) BT-958 compatible host bus adapter or an LSI Logic Ultra320 LSI53C10xx SCSI controller)
- Virtual SCSI disks with a maximum size of 950 GB
- A primary and secondary IDE channel for up to four devices
- Virtual IDE disks with a maximum size of 950 GB
- A maximum of three AMD PCnet-PCI II compatible Ethernet adapters
- Creative Labs Sound Blaster® AudioPCI emulation
- Virtual floppy drives (maximum of two), parallel and serial ports, and two USB ports
- Two-port USB 1.1 UHCI controller
- Keyboard and PS/2 mouse

## 2.9 Creating your First Virtual Machine

It is now time to create your first virtual machine. I will walk you through the steps in the Wizard and will explain all your options. I will also explain what the implications are when selecting settings other than the default.

You create your virtual machine after starting VMware Workstation by selecting New Virtual Machine from the File menu or from the main window. This will start the New Virtual Machine Wizard.

- 1. The first option that you have to select is whether to use the typical or the Custom configuration. I am assuming that you are the investigative type or an advanced user, so we will use the Custom configuration and go through it step by step.
- 2. The next window will be new to users that have worked with version 4.x. You are prompted with the choice (Figure 2.5) to either create a new virtual machine or a legacy machine that is compatible with version 4.

![](img/25fe75b93b97a021effaba85db112a52_38_0.png)

The default selection for version 5 is to create a new machine. The legacy machine can be used in version 4.x but also in VMware GSX Server, ACE 1.x and ESX Server 2.x. For more information about VMware virtual machine generations, checkout section 0.

Figure 2.5: You can still create VMs that are compatible with version 4 and GSX Server.

3. Next, select the operating system that you want to install in this virtual machine. Your selection will create the most optimized configuration for your guest operating system.

![](img/25fe75b93b97a021effaba85db112a52_38_1.png)

Figure 2.6: Always select the correct OS to get the right settings.

Selecting the incorrect operating system does not cause too many serious problems. The OS will actually run, but it could have a negative impact on the performance. You can also change the operating system later on from the virtual machine configuration settings. Based on your selection, VMware sets the defaults for your machine to what is best for your guest OS. For example, if you select Windows XP, the Wizard will propose to use an IDE disk by default, because SCSI drivers for VMware are not supported by default. If you choose SuSE Linux, VMware will propose SCSI because drivers for the VMware SCSI storage adapter are supported by this operating system. VMware will also set the amount of memory to use, such as to 256 MB, because that is enough memory to run Windows XP or SuSE Linux.

The selected operating system is also used to select the tools that you need to install in the guest, and to display additional tips if required for that operating system.

4. After selecting the guest operating system, you are prompted for the location of your virtual machine files. Create a directory per virtual machine to store all the files.

5. Your next choice is to decide how much memory to use for your virtual machine. The default of 256 MB of RAM shown below is the default for Windows XP and SuSE Linux.

![](img/25fe75b93b97a021effaba85db112a52_39_0.png)

Figure 2.7: Set the memory to your needs or accept the defaults.

The maximum amount of memory for any virtual machine is 3584 MB. If you do not have this amount of RAM in your host PC, then it is useless to select this amount of memory. Do not set the memory too low, especially during installation. The installation process of a virtual machine may notify you about insufficient memory and the performance will be very poor. A general rule for VMware virtual machines is to use as much RAM as you can, but of course not more than what you have in your physical machine. The total amount of RAM to be used in all virtual machines that run concurrently is 4 GB. More detailed explanations about memory optimization can be found in chapter 8: “Performance tuning and optimization”.

6. Next, select the choice of networking that you want for your virtual machines.

![](img/25fe75b93b97a021effaba85db112a52_40_0.png)

Figure 2.8: Select the network type for your virtual machine.

When installing Windows or Linux, it is a good idea to run them in a bridged mode during the installation. That way, they have access to the Internet (when available) on your network. You can then update them via the web during or right after the installation. It is easy to download new drivers or other software that you need for your guest operating system directly into the virtual machine.

7. Every virtual machine will support normal ATAPI IDE devices, but you will have to decide whether you want to use the Buslogic or LSI Logic SCSI adapters for your virtual SCSI environment. VMware will set a default choice based on the operating system that you have selected. There is a separate chapter on using SCSI devices for Windows, Linux, and NetWare later on in this book.

- 8. Next, you will have to select the type of disk that you will be using. You can choose to create a new virtual disk (which is what I suggest you do to get started), use an existing disk if you already have one, or use a physical disk. This last option is not recommended for most common installations.
- 9. In the next window, you have to select the Virtual Disk Type: IDE or SCSI. If you are not sure if SCSI is correctly supported by your operating system, then set it to IDE because that is supported by any known operating system.
- 10. If you have chosen to use a virtual disk in step 8, you must now select the size of the disk. Also, select if you want the disk to grow dynamically to that size, or if the disk space should be allocated when creating the virtual disk.

![](img/25fe75b93b97a021effaba85db112a52_41_0.png)

Figure 2.9: Specify the disk size and other features for your virtual disk.

The minimum size of a disk is 100 MB and the maximum is 950 GB for both IDE and SCSI.

If you have a file system that only supports files to a maximum of 2 GB (such as FAT), you will have to split the disk files onto separate 2 GB files. However, they will form a set of files that have the same name prefix and are

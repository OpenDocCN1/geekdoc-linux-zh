# Resolving Other Installation Problems



| Use This Boot Option | To Do This |
| :--- | :--- |
| **noapic** | Prevents the kernel from using the Advanced Programmable Interrupt Controller (APIC) chip. (You can use this command on motherboards known to have a bad APIC.) |
| **nofirewire** | Does not load support for FireWire |
| **noht** | Disables **Hyper-Threading**, which is a feature that enables a single processor to act as multiple virtual processors at the hard-ware level. |
| **nomce** | Disables self-diagnosis checks performed on the CPU by using Machine Check Exception (MCE). On some machines, these checks are performed too often and need to be disabled. |
| **nomount** | Does not automatically mount any installed Linux partitions in rescue mode |
| **nopass** | Does not pass the keyboard and mouse information to stage 2 of the installation program |
| **nopcmcia** | Ignores any PCMCIA controllers in system |
| **noprobe** | Disables automatic hardware detection and instead prompts the user for information about SCSI and network hardware installed on the PC. You can pass parameters to modules by using this approach. |
| **noshell** | Disables shell access on virtual console 2 (the one you get by pressing Ctrl+Alt+F2) during installation |
| **nousb** | Disables the loading of USB support during the installation. (This may be useful if the installation program hangs early in the process.) |
| **nousbstorage** | Disables the loading of the `usbstorage` module in the installation program's loader. It may help with device ordering on SCSI systems. |
| **reboot=**`b` | Changes the way the kernel tries to reboot the PC so that it can reboot even if the kernel hangs during system shutdown |
| **pci=noacpi** | Causes the kernel to not use ACPI to route interrupt requests |
| **pci=biosirq** | Causes the kernel to use BIOS settings to route interrupt requests (IRQs) |
| **rescue** | Starts the kernel in rescue mode where you get a shell prompt and can try to fix problems |
| **resolution=**`HHHHxVVV` | Causes the installer GUI to run in the specified video mode. (Make sure you replace *HHHH* and *VVV* with standard resolution numbers, such as 640x480, 800x600, 1024x768, and so on.) |
| **selinux=0** | Disables the SELinux kernel extensions |
| **serial** | Turns on serial console support during installation |
| **skipddc** | Skips the Display Data Channel (DDC) probe of monitors. (This is useful if the probing causes problems.) |
| **vnc** | Starts a VNC (Virtual Network Computing) server so that you can control the GUI installer from another networked system that runs a VNC client |

![](bbox=[0.12, 0.1, 0.87, 0.11])
# 64 Setting Up Printers

| Table 3-1 (continued) Description |
| Command | Description |
| nopcmcmia | Ignores any PCMIA controllers and instead |
| noprobe | Disables automatic hardware detection and prompts the user for information about SCSI and network hardware installed on the PC. You can pass parameters to modules by using this approach. |
| noshell | Disables shell access on virtual console 2 (the one you by pressing Ctrl+Alt+F2) during installation. |
| nousb | Disables the loading of USB support during the installation (may be useful if the installation process hangs early in the process). |
| nousbstorage | Disables the loading of usbstorage module during installation program's loader. It may help with device ordering on SCSI systems. |
| reboot=b | Changes the way the kernel tries to reboot the PC so that it can reboot even if the kernel hangs during system shutdown. |
| pci=nacpi | Causes the kernel to not use ACPI to interrupt requests (IRQs). |
| rescue | Starts the kernel in rescue mode where you get a shell prompt and can try to fix problems. |
| resolution=HHHHVVV | Causes the installer GUI to run in the specified video mode (replace HHHH and VVV with standard resolution numbers, such as 640x480, 800x600, 1024x768, and so on). |
| selinux=0 | Disables SELinux kernel extensions. |
| serial | Turns on serial console during installation. |
| skip | Skips the Display Data Channel (DDC) probe of monitors (useful if the probing causes problems). |
| text | Runs the installation program in text mode. |

# Setting Up Printers

The Fedora Core installer does not include a printer configuration step, but you can easily configure a printer from a graphical utility program. To set up printers, follow these steps:

+   1. From the graphical login screen, log in as root.

If you're not logged in as root, proceed to the next step and the printer configuration tool prompts you for the root password.
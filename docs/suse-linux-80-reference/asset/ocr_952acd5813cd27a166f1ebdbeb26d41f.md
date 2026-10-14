# Integrating the Hardware Using Modules

Select loading of kernel modules with ‘Kernel module’ only if you need support for SCSI or for PCMCIA or if you do not have an ATAPI drive. At present, appropriate modules are also swapped out as modules (e.g., IDE) or added (e.g., USB, FireWire, or file systems). Read about how modules are loaded in Section Linux on page 281. In the following submenu, choose which modules to load. Possible choices are:

+   - **A SCSI module** — if you have a SCSI hard disk or SCSI CD-ROM drive.
+   - **A CD-ROM module** — if your CD-ROM drive is *not* connected to the (E)IDE controller or the SCSI controller.
+   - **A network module** — if you want to install via NFS or FTP, but this is not discussed here.
+   - **One or more file systems** — such as ReiserFS or ext3.

> **Tip**
> 
> If you cannot find any support for your installation medium (proprietary CD-ROM drive, parallel port CD-ROM drive, network cards, PCMCIA) among the standard modules, you may find what you need on the modules floppy disk, which contains additional drivers. To do this, go to the end of the list and select the item “— More modules —”. You are then asked to insert the modules.

# Starting installation

Since you have already selected ‘Installation/System boot’, you only need to press `↵` to begin the installation.

The following items are available:

+   - **‘Start Installation/Update’** Prepare for an installation or an update of the existing system.
+   - **‘Boot Installed System’** You will probably need this item later if you encounter problems when booting your system.
+   - **‘Boot Rescue System’** This option is currently only offered for X86-compatible systems.
+   - **‘Eject CD’** Eject CD electronically.
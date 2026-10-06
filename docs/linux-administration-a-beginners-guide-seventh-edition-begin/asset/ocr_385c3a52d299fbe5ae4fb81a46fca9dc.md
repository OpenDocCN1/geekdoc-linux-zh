# APPENDIX A Creating a Linux Installer on Flash/USB Devices

The placeholder labeled <VERSION> in the filename (Fedora-Server-DVD-x86_64-<VERSION>.iso) and in the URL represents the latest version for Fedora that is available at the time you are reading this. For example, Fedora 24, the actual ISO filename will be Fedora-Server-DVD-x86_64-24.iso.

For purposes of this example, assume that the ISO file is 2.1GB. Therefore, we need to make sure that the target flash/USB-based device is at least as big. A 4GB flash drive is present in this instance.

+   Plug the flash-based device into the appropriate port on the host system.

+   You need to uniquely identify the device file that the Linux kernel associates with the flash device plugged in. It is very important that you properly identify the target device so you don't accidentally overwrite the wrong device! The dmesg command allows you to examine the Linux kernel ring buffer and provides one method for identifying the device. The most recent contents or activities in the buffer can be viewed at the tail end of the output. To view the most recent entries (lines) of the buffer,

```
# dmesg
[98492.373438] sd 4:0:0:0: [ ] Write Protect is off
..OUTPUT TRUNCATED..
[98492.381994] sdb: sdb1
[98492.391192] sd 4:0:0:0: [ ] Attached SCSI removable device
```

The output indicates that the kernel has noticed and enumerated a new device, and the device name is sdb (/dev/sdb). As an aside, we also notice that the device also has one partition-sdb1 (/dev/sdb).

+   With the previous information, we are now ready to write the ISO image file to the detected flash medium (/dev/sdb). We will use the dd utility for this purpose. Don't forget to replace <VERSION> in the command with the correct version number for your ISO file.

```
# dd if=/tmp/Fedora-Server-DVD-x86_64-<VERSION>.iso of=/dev/sdb
```

+   Once the previous command runs to completion, you will be returned to your shell prompt. You may now unplug the flash device and insert it into the appropriate port of the new system that you want to install Linux.

+   If necessary, configure the BIOS or the UEFI of the target system to boot off the flash-based device. Once booted into the installer, follow the installation steps as described in Chapter 2, or as specified by the distro vendor.
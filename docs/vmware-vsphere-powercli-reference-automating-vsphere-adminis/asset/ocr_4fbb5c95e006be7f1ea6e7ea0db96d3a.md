All the steps involved in expanding the system partition using a helper virtual machine (normally done by hand) are now fully automated. The following tasks are performed automatically for you:

+   - Extend the virtual disk in VM001.
- Add the virtual disk to the helper virtual machine VM002.
- Power on the helper virtual machine VM002.
- Expand the partition on the helper virtual machine VM002.
- Remove the virtual disk from the helper virtual machine VM002.
- Shut down the helper virtual machine VM002.

# Changing Other Hardware

When it's time to install software from a CD or ISO image, a drive will need to be added to the VM if it doesn't have one already. A new drive can be added to your virtual machine using the New-CDrive cmdlet. You can connect the drive to an ISO image file:

```
Get-VM VM001 | New-CDrive -IsoPath '
  "[Datastore01] ISO/parted-live.iso" -StartConnected
```

or to the host's drive:

```
Get-VM VM001 | New-CDrive -HostDevice '\n  "/vmfs/devices/cdrom/vmhba32:C0:L0"'
```

For security purposes, it is a good practice to remove all virtual hardware from the VM that is not used. For example, VMs rarely contain a floppy drive, as it's very unlikely that one will ever be needed. But there may be a need for a temporary floppy drive for a legacy application. To connect a floppy drive, use the New-FloppyDrive cmdlet. To connect a floppy image to our VM001, with following:

```
Get-VM VM001 | New-FloppyDriveImagePath '\n  "[Datastore01] ISO/floppy.flp"
```

A new floppy drive can be created by using the New-FloppyImagePathPath parameter and specifying a datastore path to the new floppy image:

```
Get-VM VM001 | New-FloppyImagePathPath '\n  "[Datastore01] ISO/myNewFloppy.flp"
```
Hotplug devices, on the other hand, are designed to be connected and disconnected dynamically while the system is up and running. Software on the Linux system detects the changes to the system as these types of devices are attached and detached. The system will recognize the device when it is connected and load the appropriate modules. Several Linux components are needed to do this:

+   - sysfs
+   - dbus
+   - hdid
+   - udev

# ## Accelerated Review

+   - PC systems need persistent, long-term storage media to store information.
+   - Floppy diskettes save data on a coated Mylar disk.
+   - Floppy drives are all but completely phased out.
+   - Hard disks use coated aluminum platters to store data.
+   - Drive geometry consists of the following parameters:
+     - Heads
+     - Cylinders
+     - Sectors Per Track
+   - IDE hard drives have the disk controller integrated into the drive itself.
+   - IDE uses master and slave drives.
+   - An IDE channel can have only one master drive.
+   - Most PCs provide two IDE channels (Primary and Secondary).
+   - SATA has almost completely replaced IDE storage devices.
+   - SATA drives are much faster than the fastest ATA drives.
+   - SATA drives are not subject to the master/slave configuration rules.
+   - Each SATA drive in your system has its own dedicated hard disk channel that greatly enhances speed and throughput.
+   - SATA cabling is much simpler, using a seven-pin connector.
+   - SATA devices can transfer data at rates from 150 MBps/sec up to a maximum of 600 MBps/sec.
+   - The SATA drive connected to the SATA0 connector on the system motherboard will be used as the boot drive by default because it will be assigned an ID of 0.
+   - SCSI hard drives are used mostly in server systems.
+   - SCSI devices are connected in a chain.
+   - Each SCSI device in the chain is assigned a SCSI ID.
Finally, here's an example of the device information for an Ultra system displayed using the dmesg command:

```
# dmesg
Aug  1 12:08:04 ultra5 genunix: [ID 540533 kern.notice]: \
SunOS Release 5.8 Version Generic_108528-07 64-bit
Aug  1 12:08:04 ultra5 genunix: [ID 913631 kern.notice] \
Copyright 1983-2001 Sun Microsystems, Inc.  All rights reserved.
Aug  1 12:08:04 ultra5 genunix: [ID 678236 kern.info] \
Ethernet address = 8:0:20:a2:63:82
Aug  1 12:08:04 ultra5 unix: [ID 389951 kern.info] mem = 131072K (0x8000000)
Aug  1 12:08:04 ultra5 unix: [ID 930857 kern.info] avail mem = 122142720
Aug  1 12:08:04 ultra5 rootnex: [ID 466748 kern.info] root nexus = Sun Ultra 5/10 UPA/PCI \
(UltraSPARC-IIi 270MHz)
Aug  1 12:08:04 ultra5 rootnex: [ID 349649 kern.info] pcipsy0 at root: UPA 0x1f 0x0
Aug  1 12:08:04 ultra5 genunix: [ID 936769 kern.info] pcipsy0 is /pci@1f,0
Aug  1 12:08:04 ultra5 pcipsy: [ID 370704 kern.info] PCI-device: pci@1,1, simba0
Aug  1 12:08:04 ultra5 genunix: [ID 936769 kern.info] simba0 is /pci@1f,0/pci@1,1
Aug  1 12:08:04 ultra5 pcipsy: [ID 370704 kern.info] PCI-device: pci@1, simba1
Aug  1 12:08:04 ultra5 genunix: [ID 936769 kern.info] simba1 is /pci@1f,0/pci@1
Aug  1 12:08:20 ultra5 simba: [ID 370704 kern.info] PCI-device: ide@3, uata0
..... <the output has been truncated>
```

Use the output of the prtconf and sysdef commands to identify which disk, tape, and CD-ROM devices are connected to the system. As shown in the previous examples, some devices display the driver not attached message next to the device instance. This message does not always mean that a driver is unavailable for this device. It means that no driver is currently attached to the device instance because there is no device at this node, or the device is not in use. The OS automatically loads drivers when the device is accessed, and it unloads them when it is not in use.

The system determines what devices are attached to it at startup. This is why it is important to have all peripherals powered on at startup, even if they are not currently being used. During startup, the kernel configures itself dynamically, loading needed modules into memory. Device drivers are loaded when devices, such as disk and tape devices, are accessed for the first time. This process is called auto-configuration, because all kernel modules are loaded automatically if needed. As described in Chapter 2, the system administrator can customize the way in which kernel modules are loaded by modifying the /etc/system file.
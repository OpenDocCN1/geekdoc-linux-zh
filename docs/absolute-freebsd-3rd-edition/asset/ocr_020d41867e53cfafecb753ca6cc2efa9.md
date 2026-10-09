```
6 luname: ATA WDC WD1003FBYZ-01OFB0 WD-WCAW36478143
7 lunit: 50014ee25e60dab5
8 ident: WD-WCAW36478143
9 rotationrate: 7200
10 fwsectors: 63
fwheads: 255
```

This hard drive provides a disk device called da0 ❶. The mediasize field gives its size in bytes and converts it to a more convenient 932GB ❷.

This disk claims to have a sector size of 512 bytes ❸. Many disks lie about their sector size. Check the drive manufacturer's documentation to determine the actual sector size. Drives might offer a Stripe size value of 4,096 to indicate that they're actually 4K drives.

A GEOM class's mode looks an awful lot like file permissions ❹, but it's really the number of GEOM classes reading from (r2) and writing to (w2) the device, plus the number of devices that have requested exclusive access to the device (e3).

The descr field ❺ offers the drive's model number.

The luname field ❻ gives the model number plus the serial number. Yes, it's a combination of the descr and ident fields. The hard drive really, really wants you to believe this is its name and identifier.

The lunit ❼ gives the logical-unit-number (LUN) identifier, which describes how this drive attaches to this host.

The disk's ident ❽ is the drive's serial number.

The rotationrate ❾ tells us how fast this drive spins. It's a 7,200 RPM disk. Nonspinning disks, like SSDs, have a rotationrate of 0.

The fwsectors and fwheads fields ❿ give us the drive geometry. These are examples of the lies mentioned in the beginning of this chapter. Even SSDs offer these values.

Some drives offer less information. Virtual disks offer almost no information, and anything they do say, you can't trust. (While the VM system might say this disk offers 32,212,254,720 512-byte sectors, who knows what the actual disk beneath the virtual disk has?)
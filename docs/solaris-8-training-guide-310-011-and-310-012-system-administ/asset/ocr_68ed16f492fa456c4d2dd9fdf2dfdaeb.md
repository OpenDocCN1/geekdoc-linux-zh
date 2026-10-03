| Parameter | Description |
|---|---|
| device-arguments | A text string whose format depends on the particular device. It can be used to pass additional information to the device's software. In this example:
`/sbus@1f,0/scsi@2,1/sd@3,0:a`

The argument for the disk device is "a." The software driver for this device interprets its argument as a disk partition, so the device pathname refers to partition "a" on that disk. |

The OpenBoot command show-devs is used to obtain information about devices and to display device pathnames. This command displays all the devices known to the system directly beneath a given device in the device hierarchy. show-devs used by itself shows the entire device tree. The syntax is as follows:

```
show-devs [device path]
```

An example is as follows:

```
ok show-devs
```

The system outputs the following information:

```
/TI,TMS390Z50@f,f8fffffc
/eccmemctl@f,0
/virtual-memory@0,0
/memory@0,0
/obio
/iommu@f,e0000000
/openprom
/aliases
/options
/packages
/obio/power@0,a01000
/obio/auxio@0,800000
/obio/SUNW,fdtwo@0,700000
/obio/interrupt@0,400000
/obio/counter@0,300000
/obio/eeprom@0,200000
/obio/zs@0,0
/obio/zs@0,100000
/iommu@f,e0000000/sbus@f,e0001000
/iommu@f,e0000000/sbus@f,e0001000/cgsix@2,0
/iommu@f,e0000000/sbus@f,e0001000/SUNW,DBRIe@f,8010000
/iommu@f,e0000000/sbus@f,e0001000/SUNW,bpp@f,4800000
/iommu@f,e0000000/sbus@f,e0001000/ledma@f,400010
/iommu@f,e0000000/sbus@f,e0001000/espdma@f,400000
/iommu@f,e0000000/sbus@f,e0001000/SUNW,DBRIe@f,8010000/mmcodec
/iommu@f,e0000000/sbus@f,e0001000/ledma@f,400010/le@f,c00000
```
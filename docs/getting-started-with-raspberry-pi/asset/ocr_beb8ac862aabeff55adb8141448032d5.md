+   1. `storage_probe()` registers a virtual SCSI adapter by calling `scsi_add_host()`, supplying a private data structure called `us_data` as argument. `scsi_add_host()` returns a `Scsi_Host` structure for this virtual adapter, with space at the end for `us_data`.

+   2. It starts a kernel thread called `usb-storage` to handle all SCSI commands queued to the virtual adapter.

+   3. It schedules a kernel thread called `usb-stor-scan` that requests the SCSI middle-level layer to scan the bus for attached devices.

+   4. The device scan initiated in Step 3 discovers the presence of the inserted pen drive and binds the upper-level SCSI disk driver (`sd.c`) to the device. This results in the invocation of the SCSI disk driver’s probe method, `sd_probe()`.

+   5. The `sd` driver allocates a `/dev/sd*` node to the disk. From this point on, applications use this interface to access the USB disk. The SCSI subsystem queues disk commands to the virtual adapter, which the usb-storage kernel thread handles using appropriate URBs.

Now that you know the basics, let’s dissect Listing 11.6, looking at the data structure additions first. The listing adds a `snam` field to the `Scsi_Host` structure to hold the associated SCSI `/dev` name that we are interested in. It also adds a private field to the `usb_interface` structure to associate each USB interface with its `us_data`. Because `us_data` is relevant only for storage devices, we need to ensure the validity of the private field of a USB interface before accessing it as `us_data`. For this, Listing 11.6 adds a magic string, “disk,” to `us_data`.

The `usbf$` modification in Listing 11.6 (to `drivers/usb/core/devices.c`) pulls out the `us_data` associated with each interface via the private data field of its `usb_interface`. It then latches on to the associated `Scsi_Host` using the `container_of()` function, because as you saw in Step 1 previously, `usb_data` is glued to the end of the corresponding `Scsi_Host`. As you further saw in Step 5, `Scsi_Host` contains the `/dev` node names that the `sd` and `sr` drivers populate. `Usbf$` stitches together an “N:” line using this information.

The following is the `/proc/bus/usb/devices` output after integrating the changes in Listing 11.6 and attaching a PNY USB pen drive, an Addonics CD-ROM drive, and a Seagate hard disk to a laptop via a USB hub. The “N:” lines announce the identity of the `/dev` node corresponding to each device:

Code View:

```
```bash
bash> cat /proc/bus/usb/devices
```
```
.. .
T:	Bus=04 Lev=02 Prnt=02 Port=00 Cnt=01 Dev#=  3 Spd=480 MxCh=  0
N:	Device=sda(Disk)
D:	Ver= 2.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS=64 #Cfgs=  1
P:	Vendor=154b ProdID=0002 Rev= 1.00
S:	Manufacturer=PNY
S:	Product=USB 2.0 FD
S:	SerialNumber=6E5C07005B4F
C:	#Ifs= 1 Cfg#= 1 Atr=80 MxPwr=  0mA
I*	If#= 0 Alt= 0 #EPS= 2 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage

T:	Bus=04 Lev=02 Prnt=02 Port=01 Cnt=02 Dev#=  5 Spd=480 MxCh=  0
N:	Device=sr0(CDR0M)
D:	Ver= 2.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS=64 #Cfgs=  1
P:	Vendor=0bf6 ProdID=a002 Rev= 3.00
S:	Manufacturer=Addonics
```
```

The steps involved in device recognition by udev are shown in Figure 8-5.

![](img/f332344337ca8bf6846cb313a66ee0b3_264_0.png)

*Figure 8-5 Sequence of attaching new devices with hotplug*

The steps are:

1. A new device is added and a machine check occurs.
2. The machine check handler informs the common I/O layer of the new device.
3. Information about the added device is acquired in the common I/O. A new entry is created in sysfs.
4. Hotplug is called.
5. udev is called.
6. udev references sysfs.
7. The device file is created.

Sysfs offers an interface to the user space for accessing the data structure in the kernel space. Sysfs can dynamically add and delete via both the hotplug agent and by user operations. It also allows for option setting (log level, for example) of the device and driver and confirmation of device status (such as on or offline).

The Sysfs contains virtual configuration and control files, for example:

- Example of configuring an OSA device
  ```
  # echo "0.0.0769,0.0.076a,0.0.076b" > /sys/bus/ccwgroup/drivers/geth/group
  # echo 1 > /sys/bus/ccwgroup/drivers/geth/0.0.0769/online
  ```

- Example of the changing log level
  ```
  # echo 2 > /sys/bus/ccw/drivers/zfcp/loglevel_qdio
  ```

- Example of making channel path offline/online
  ```
  # echo offline > /sys/devices/css0/chp0.xx/status
  # echo online > /sys/devices/css0/chp0.xx/status
  ```

- Example of changing option setting
  ```
  # echo 1 > /sys/devices/geth/0.0.e18c/layer2
  ```

## 8.2.3 Device drivers

The following are the device drivers, their corresponding kernel modules (if applicable), and descriptions and characteristics that are common in a Linux on System z configuration:

- DASD device driver
    - Kernel modules: dasd_mod, dasd_eckd_mod, dasd_fba_mod.
    - A device driver that is used to access channel-attached DASD devices.
    - Channel subsystem processes path control and error recovery. Linux does not consider the existence of path.
    - Linux controls it by using device file /dev/dasda.
        - The first partition is /dev/dasdx1, the second partition is /dev/dasdx2.
        - The maximum number of partitions is 3.

- zfcp device driver
    - A device driver that is used to access Fibre Channel attached SCSI devices.
    - A channel subsystem is not used. The buffer I/O of QDIO is used instead. Linux has to process path control and error recovery by itself because of this.
    - Information about the Host Bus Adapter (HBA) and the logical unit number (LUN) on the storage server side is needed in order to recognize a LUN.
    - Linux controls recognize the LUN by using the device file, /dev.

- Network device driver
    - Network devices are controlled by network device drivers.
    - The device file and major/minor numbers are created in the same way as disk and tape.
    - The interface is created and related to a device.
    - The default name of an interface depends on the type of interface, for example, Ethernet (eth0, eth1), HipérSockets (hsio, hsi). The name of the interface can be changed <geth>.
    - Device drivers are used to access the OSA-Express of QDIO mode and HipérSockets.
    - Channel subsystems are not used. Buffer I/O of QDIO is used instead.
    - The qeth device driver needs 3 subchannels to recognize an OSA device:
        - An even number of control read devices.
        - The control write devices must be the device bus-ID of the read subchannel plus one.
        - Data devices can be any free device bus-ID on the same CHPID.

## 8.2.4 Confirming status of channel path and devices

This section describes the command and files for status confirmation of devices. It is possible to confirm the devices' status provided by sysfs. It is important to confirm the status, even under normal circumstances.

![](img/f332344337ca8bf6846cb313a66ee0b3_266_0.png)

| Category | Commands/files | Description and contents |
| :--- | :--- | :--- |
| **General** | `lscss` | The device status that common I/O manages |
| | `/etc/sysconfig/hardware/*` | Device information |
| **DASD** | `lsdasd` | Composition information about DASD |
| | `/sys/bus/ccw/drivers/dasd-eckd/0.0.<addr>` | Composition information about DASD |
| | `/proc/dasd` | Composition information and statistical information about DASD |
| **FCP** | `lsscsi` | Information on SCSI devices |
| | `/sys/bus/ccw/drivers/zfcp/0.0.<addr>` | Composition information about SCSI devices |
| | `/proc/scsi/IBMtape, /proc/scsi/IBMchanger` | FCP tape device information |
| **Network** | `lsqeth` | Composition information on the qeth network devices |
| | `/sys/bus/ccwgroup/drivers/qeth/0.0.<addr>` | qeth network devices information |
| | `/proc/qeth` | qeth network devices information |

It is possible to confirm the status of the channel path and devices by using the `lscss` command. See Example 8-2.

### Example 8-2 Confirming channel path status and device status

```
Device        Subchan.    DevType CU Type Use    PIM PAM POM CHPIDs
0.0.0009      0.0.0000    0000/00 3215/00 yes     80  80  FF      00000000 00000000
0.0.000C      0.0.0001    0000/00 2540/00          80  80  FF      00000000 00000000
0.0.000D      0.0.0002    0000/00 2540/00          80  80  FF      00000000 00000000
0.0.000E      0.0.0003    0000/00 1403/00          80  80  FF      00000000 00000000
0.0.0190      0.0.0004    3390/0A 3990/E9          F0  F0  FF      C0C2C1C3 00000000
0.0.019E      0.0.0005    3390/0A 3990/E9          F0  F0  FF      C0C2C1C3 00000000
0.0.019D      0.0.0006    3390/0A 3990/E9          F0  F0  FF      C0C2C1C3 00000000
0.0.0191      0.0.0007    3390/0A 3990/E9          F0  F0  FF      C0C2C1C3 00000000
0.0.05B0      0.0.0008    1732/01 1731/01 yes      80  80  FF      A9000000 00000000
0.0.05B1      0.0.0009    1732/01 1731/01 yes      80  80  FF      A9000000 00000000
0.0.05B2      0.0.000A    1732/01 1731/01 yes      80  80  FF      A9000000 00000000
0.0.0240      0.0.000B    1732/01 1731/01 yes      80  80  FF      BE000000 00000000
0.0.0241      0.0.000C    1732/01 1731/01 yes      80  80  FF      BE000000 00000000
0.0.0242      0.0.000D    1732/01 1731/01 yes      80  80  FF      BE000000 00000000
0.0.0128      0.0.000E    3390/0A 3990/E9 yes      F0  F0  FF      C0C2C1C3 00000000
0.0.0129      0.0.000F    3390/0A 3990/E9 yes      F0  F0  FF      C0C2C1C3 00000000
0.0.3B0C      0.0.0014    1732/03 1731/03          80  80  FF      B6000000 00000000
```

### Channel path status

You would confirm the physical path status by using the `lscss` command and looking at the columns labeled PIM, PAM, and POM. These are a part of the path status information that are included in the subchannel information block. See Figure 8-6.

![](img/f332344337ca8bf6846cb313a66ee0b3_268_0.png)

Figure 8-6 Confirming channel path status

### Confirming device status

To confirm the status of DASD, use the `lsdasd` command found in /proc/dasd/devices.

Output from this command will be similar to that found in Example 8-3.

#### Example 8-3 Confirming DASD status

| Device | Type | (at) | Volume | Status | Details |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0.0.c128 | (ECKD) | at | (94: 0) | is dasda : active | at blocksize 4096, 601020 blocks, 2347 MB |
| 0.0.c129 | (ECKD) | at | (94: 4) | is dasdb : active | at blocksize 4096, 601020 blocks, 2347 MB |
| 0.0.c12a | (ECKD) | at | (94: 8) | is dasdc : active | at blocksize 4096, 601020 blocks, 2347 MB |

To confirm the FCP device status, use the `lsscsi` command, as shown in Example 8-4.

#### Example 8-4 Confirming FCP device status

```
# lscssi -v
sysfsroot: /sys
[0:0:1:0]      disk      IBM      2105800      .112  /dev/sda
dir: /sys/bus/scsi/devices/0:0:1:0
[/sys/devices/css0/0.0.0007/0.0.f441/host0/0:0:1:0]
```

To confirm OSA status, use the `lsqeth` command (this command is only for SLES), as shown in Example 8-5.

#### Example 8-5 Output of the lsqeth command - confirming OSA devices

```
Device name            : eth0
----------------------
card_type          : GuestLAN QDIO
cdev0             : 0.0.05a0
cdev1             : 0.0.05a1
cdev2             : 0.0.05a2
chpid             : A9
online            : 1
portno            : 0
route4            : no
route6            : no
checksumming      : sw checksumming
state             : UP (LAN ONLINE)
priority_qeueuing : always queue 2
fake_1l           : 0
fake_broadcast    : 0
buffer_count      : 16
add_hhlen         : 0
layer2            : 0
large_send        : no
```

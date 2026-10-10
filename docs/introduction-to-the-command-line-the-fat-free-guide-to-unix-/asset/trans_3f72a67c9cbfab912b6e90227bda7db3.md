

# ioscan

**用途：** 列出 HP-UX 系统上的硬件。

**用法语法：** `ioscan [OPTIONS]`

```bash
# ioscan
H/W Path Class Description
=========================================================
8 bc I/O Adapter
8/0 ext_bus GSC add-on Fast/Wide SCSI Interface
8/0.5 target
8/0.5.0 disk SEAGATE ST34371W
8/0.7 target
8/0.7.0 cti Initiator
8/0.8 target
8/0.8.0 disk SEAGATE ST318436LC
8/4 ba PCI Bus Bridge - GSCtoPCI
8/4/1/0 lan HP J3515A HSC 10/100Base-TX D-Class
1 port Core I/O Adapter
8/16 ba
8/16/0 ext_bus Built-in Parallel Interface
8/16/4 tty Built-in RS-232C
8/16/5 ext_bus Built-in SCSI
8/16/5.0 target
8/16/5.0.0 tape HP C1537A
8/16/5.2 target
8/16/5.2.0 disk SONY CD-ROM CDU-76S
8/16/5.7 target
8/16/5.7.0 cti Initiator
8/16/6 lan Built-in LAN
8/16/7 ps2 Built-in Keyboard/Mouse
8/20 ba Core I/O Adapter
8/20/2 tty Built-in RS-232C
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_168_0.png)

`ioscan` 显示安装在 HP-UX 系统上的硬件信息。上述示例展示了该命令的典型输出，其中显示了系统硬件概况的相关信息。

**常见用法示例：**

- `ioscan`：显示简单的硬件列表
- `ioscan -f`：显示详细的硬件列表

# lsdev

**用途：** 列出 AIX 系统上的硬件。

**用法语法：** `lsdev [OPTIONS]`

```bash
# lsdev
L2cache0    Available   LG-19--00     L2 Cache
cd0         Available   LG-00         IDE DVD-ROM Drive
en0         Available   1L-08         Standard Ethernet Network Interface
en1         Defined     1J-08         Standard Ethernet Network Interface
ent0        Available   1L-08         10/100 Mbps Ethernet PCI Adapter II
ent1        Available   1J-08         10/100/1000 Base-TX PCI-X Adapter
et0         Defined     1L-08         IEEE 802.3 Ethernet Network Interface
et1         Defined     1J-08         IEEE 802.3 Ethernet Network Interface
fd0         Available   01-D1--00-00  Diskette Drive
fda0        Available   01-D1         Standard I/O Diskette Adapter
hd1         Defined             Logical volume
hd2         Defined             Logical volume
hd3         Defined             Logical volume
hd4         Defined             Logical volume
hd5         Defined             Logical volume
hd6         Defined             Logical volume
hd8         Defined             Logical volume
hd10opt     Defined             Logical volume
hd11admin   Defined             Logical volume
hd9var      Defined             Logical volume
hdisk0      Available   1S-08--00-5,0  16 Bit LVD SCSI Disk Drive
hdisk1      Defined     1S-08--00-8,0  Other SCSI Disk Drive
hdisk2      Available   1S-08--00-8,0  16 Bit LVD SCSI Disk Drive
ide0        Available   LG-19         ATA/IDE Controller Device
...
```

使用 `lsdev` 列出 AIX 上的设备

`lsdev` 显示安装在 AIX 系统上的硬件信息。上述示例展示了该命令的典型输出，其中包含有关本地系统上安装硬件的信息。

**常见用法示例：**

- `lsdev`：显示简单的硬件列表

# lspci

**用途：** 列出 Linux 系统上的 PCI 设备。

**用法语法：** `lspci [OPTIONS]`

```bash
# lspci
00:00.0 Host bridge: Intel Corporation 82945G/GZ/P/PL Memory Controller
Hub (rev 02)
00:01.0 PCI bridge: Intel Corporation 82945G/GZ/P/PL PCI Express Root
Port (rev 02)
00:02.0 VGA compatible controller: Intel Corporation 82945G/GZ
Integrated Graphics Controller (rev 02)
00:02.1 Display controller: Intel Corporation 82945G/GZ Integrated
Graphics Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express
Port 1 (rev 01)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express
Port 2 (rev 01)
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_170_0.png)

`lspci` 列出 Linux 系统上的 PCI 设备。在上述示例中，显示了一个基本的 PCI 设备列表。使用 `-v` 选项可以生成更详细的列表，如下一个示例所示。

```bash
# lspci -v
00:00.0 Host bridge: Intel Corporation 82945G/GZ/P/PL Memory Controller
Hub (rev 02)
	Subsystem: Dell Device 01ad
	Flags: bus master, fast devsel, latency 0
	Capabilities: [50] Vendor Specific Information <?>
	Kernel driver in use: agpgart-intel
	Kernel modules: intel-agp

00:01.0 PCI bridge: Intel Corporation 82945G/GZ/P/PL PCI Express Root
Port (rev 02)
	Flags: bus master, fast devsel, latency 0
	Bus: primary=00, secondary=01, subordinate=01, sec-latency=0
	Memory behind bridge: fe900000-fe9ffff
	Capabilities: [88] Subsystem: Intel Corporation Device 0000
	Capabilities: [80] Power Management version 2
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_170_1.png)

**常见用法示例：**

- `lspci`：显示简单的 PCI 设备列表
- `lspci -v`：显示详细的 PCI 设备列表

# pciconf

**用途**：列出 BSD 系统上的 PCI 设备。

**用法语法**：`pciconf [OPTIONS]`

```bash
# pciconf -lv | less
host0@pci0:0:0:0:  class=0x060000 card=0x00000000 chip=0x12370886
rev=0x02 hdr=0x00
  vendor   = 'Intel Corporation'
  device   = '82440/1PX 440FX (Natoma) System Controller'
  class    = bridge
  subclass = HOST-PCI
isa0@pci0:0:1:0:  class=0x060100 card=0x00000000 chip=0x70008086
rev=0x00 hdr=0x00
  vendor   = 'Intel Corporation'
  device   = 'PIIX3 PCI-to-ISA Bridge (Triton II) (82371SB)'
  class    = bridge
  subclass = PCI-ISA
atapci0@pci0:0:1:1:  class=0x01018a card=0x00000000 chip=0x71118086
rev=0x01 hdr=0x00
  vendor   = 'Intel Corporation'
  device   = 'PIIX4/4E/4M IDE Controller (82371AB/EB/MB)'
  class    = mass storage
  subclass = ATA
vgapci0@pci0:0:2:0:  class=0x030000 card=0x00000000 chip=0xbeef80ee
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_171_0.png)

`pciconf` 命令显示 BSD 系统上的 PCI 设备。上述示例演示了在 BSD 系统上列出 PCI 设备。

> **注意**
>
> *在某些 BSD 系统中，可以使用 `pcidump` 或 `devinfo` 命令代替 `pciconf` 命令。*

**常见用法示例：**

- `pciconf -lv`：显示完整的 PCI 设备列表

# lsusb

**用途：** 列出 Linux 系统上的 USB 设备。

**用法语法：** `lsusb [OPTIONS]`

```bash
# lsusb
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 004: ID 0930:6544 Kingston DataTraveler 2.0 Stick (2GB)
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 003: ID 0461:4d15 Dell Optical Mouse
Bus 002 Device 002: ID 413c:2105 Dell Model L100 Keyboard
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
```

使用 `lsusb` 显示 USB 设备列表

`lsusb` 列出 Linux 系统上的 USB 设备。不带选项执行 `lsusb` 将显示本地系统上所有 USB 设备的简单列表，如上例所示。

可以使用 `-v` 选项与 `lsusb` 一起显示 USB 设备的详细列表，如下一个示例所示。

```bash
# lsusb -v | less

Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
  Device Descriptor:
    bLength            18
    bDescriptorType     1
    bcUSB             1.10
    bDeviceClass         9 Hub
    bDeviceSubClass      0 Unused
    bDeviceProtocol    0 Full speed (or root) hub
    bMaxPacketSize0      64
    idVendor    0x1d6b Linux Foundation
    idProduct   0x0001 1.1 root hub
    bcDevice            2.06
...
```

显示详细的 USB 设备列表

**常见用法示例：**

- `lsusb`：显示 USB 设备
- `lsusb -v`：显示详细的 USB 设备列表
- `lsusb -t`：以树状模式显示 USB 设备

# dmidecode

**用途：** 显示系统中设备的详细信息。

**用法语法：** `dmidecode [OPTIONS]`

```bash
# dmidecode
SMBIOS 2.31 present.
45 structures occupying 1654 bytes.
Table at 0x000E0010.

Handle 0x0000, DMI type 0, 20 bytes
BIOS Information
    Vendor: Phoenix Technologies LTD
    Version: 6.00
    Release Date: 04/17/2006
    Address: 0xE7C70
    Runtime Size: 99216 bytes
    ROM Size: 64 KB
    Characteristics:
        ISA is supported
        PCI is supported
        PC Card (PCMCIA) is supported
        PNP is supported
        APM is supported
        BIOS is upgradeable
        BIOS shadowing is allowed
        ESCD support is available
        USB legacy is supported
        Smart battery is supported
        BIOS boot specification is supported

Handle 0x0001, DMI type 1, 25 bytes
System Information
    Manufacturer: VMware, Inc.
    Product Name: VMware Virtual Platform
    Version: None
...
```

以树状视图显示设备列表

`dmidecode` 显示系统中设备的详细列表。上述示例演示了该命令的典型输出，其中包含有关系统硬件的详细信息。

![](img/8f33496304c637dbf51ff6ddc3c7ff29_173_0.png)

> `dmidecode` 命令的输出可能相当长。输入 `dmidecode | more` 将分页显示输出。

**常见用法示例：**

- `dmidecode`：显示系统中设备的详细信息


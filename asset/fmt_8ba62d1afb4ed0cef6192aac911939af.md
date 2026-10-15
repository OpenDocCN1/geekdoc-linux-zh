
# 第四部分：管理设备

```
SUNW,Ultra-5_10
  packages (driver not attached)
    terminal-emulator (driver not attached)
    deblocker (driver not attached)
    obp-lftp (driver not attached)
    disk-label (driver not attached)
    SUNW,builtrin-drivers (driver not attached)
    sun-keyboard (driver not attached)
    ufs-file-system (driver not attached)
  chosen (driver not attached)
    openprom (driver not attached)
      client-services (driver not attached)
  options, instance #0
    aliases (driver not attached)
    memory (driver not attached)
    virtual-memory (driver not attached)
  pci, instance #0
    pci, instance #0
      ebus (driver not attached)
        auxio (driver not attached)
        power (driver not attached)
        SUNW,pll (driver not attached)
        se, instance #0
        su, instance #0
        su, instance #1
        ecpp (driver not attached)
        fdhree (driver not attached)
        eeprom (driver not attached)
        flashrom (driver not attached)
        SUNW,CS4231, instance #0
  network, instance #0
    SUNW,m64b, instance #0
  ide, instance #0
    disk (driver not attached)
    cdrom (driver not attached)
    dad, instance #0
    atapicid, instance #2
pci, instance #0
  pci, instance #0
    pci1108e,1000 (driver not attached)
      SUNW,hme, instance #1
      SUNW,isptwo, instance #0
```

## 第 14 章：设备与资源管理

`sd` (driver not attached)

`st` (driver not attached)

`SUNW, UltraSPARC-III` (driver not attached)

`pseudo, instance #0`

永远不要对驱动程序“未挂载”（not attached）到特定设备的消息而感到恐慌。因为在 Solaris 10 中，驱动程序仅按需加载，因此只有那些正在活动使用的设备才会加载其驱动程序。当设备不再被使用时，驱动程序将从内存中卸载。这是一个非常高效的内存管理策略，通过在设备不再使用时释放其内存来优化 RAM 的使用率。在 Ultra 5 的情况下，你可以从前面的代码中看到 PCI 总线和 IDE 磁盘驱动器等设备已经挂载了设备驱动程序，并且在运行 `prcntf config` 时正在被使用。

对于 x86 系统，情况会有不同：

+ 系统配置：Sun Microsystems i86pc

内存大小：128 Megabytes

系统外设（软件节点）：

`i86pc`

+ `boot` (driver not attached)

`memory` (driver not attached)

`aliases` (driver not attached)

`chosen` (driver not attached)

`i86pc-memory` (driver not attached)

`di86pc-mmu` (driver not attached)

`openproc` (driver not attached)

`options, instance #0`

`packages` (driver not attached)

`delayed-writes` (driver not attached)

`tu-props` (driver not attached)

`isa, instance #0`

`motherboard` (driver not attached)

`asy, instance #0`

`lp` (driver not attached)

`asy, instance #0`

`fdc, instance #0`

`fd, instance #0`

`fd, instance #1` (driver not attached)

`kd` (driver not attached)

`bios` (driver not attached)

`bios` (driver not attached)

`npCTL, 0041` (driver not attached)

`npCTL, 7002` (driver not attached)

`kd, instance #0`

`chanmux, instance #0`

`pci, instance #0`

`pci8086, 1237` (driver not attached)

```
pci8086,7000 (driver not attached)
pci-ide, instance #0
ata, instance #0
cmdk, instance #0
sdi, instance #1
pci10ec,8023 (driver not attached)
pci5333,8901 (driver not attached)
used-resources: (driver not attached)
objmgr, instance #0
pseudo, instance #0
```

### 启动时间

OpenBoot 监控器具有在启动前诊断设备上硬件错误的能力。这对于识别连接性问题（例如未终止的 SCSI 链）特别有用，也可以用于识别功能性问题（例如设备是否有响应）。`ok` 命令还会强制进行自检。启动后，查看系统消息也是很有用的，你可以通过使用 `dmesg` 命令或检查 `/var/log/messages` 文件来获取信息。它显示了启动时成功挂载的所有设备列表，以及检测到的任何错误消息。以下是 SPARC 架构的 `dmesg` 输出：

```
dmesg
Jan 17 13:06
cpu0: SUNW,UltraSPARC-III (rev 0x12 clock 270 MHz)
SunOS Release 5.10 Generic-103640-19
UNIX(R) System Release 4.0
Copyright (c) 1983-2004, Sun Microsystems, Inc.
mem = 131072K (0x20000)
Ethernet address = 8:0:20:93:b0:65
pci1011,240: SUNW,hme: Using Transceiver
10 Mbps half-duplex Link Up
pcmia: no PCIA adapters found
```

`dmesg` 执行性能测试，设置网络接口的以太网地址，并初始化 PCI 总线。对于 SPARSE 系统，设置以太网地址至关重要，因为以太网地址存储在 PROM 中。随后识别 IDE 磁盘并映射到物理设备，标准输入设备（键盘和鼠标）被激活，启动序列大部分已完成。然而，x86 系统的输出略有不同：

```
Jan 17 08:32
SunOS Release 5.10 Generic [UNIX(R) System V 4.0]
Copyright (c) 1983-2004, Sun Microsystems, Inc.
mem = 130688K (0x7fa000)
avail mem = 11440
pci0 at root
nexus = i86pc
root = Ultra 5/10 UPA
target 0 lun 0
model = ATAPI, stat 50
cfg = 0x85,cyl 0,hd 0,sec63
minpio = 240,minflow = 120
valid = 0x7,dwma = 0x4
ata_set_feature: (0x66,0x0) failed
```

## 系统运行时

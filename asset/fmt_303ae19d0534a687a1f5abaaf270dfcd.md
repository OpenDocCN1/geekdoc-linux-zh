
引导程序负责将 UNIX 内核加载到内存并将系统控制权交给它。`boot`命令必须访问 OpenBoot 参数 `boot-device`。分配给启动设备的别名（`disk` 或 `disk#`）告诉引导设备去哪里寻找内核以及如何启动它。例如，别名 `disk` 提供了启动路径 `/sbus/1f800000/esp@0,40000/sd@3,0:a`。

## boot 命令

非交互启动 (`boot`) 使用启动路径的默认值自动启动系统。在 OpenBoot 提示符下输入以下命令启动非交互启动：

```
ok boot
```

系统将在无需更多交互的情况下启动。

交互式启动 (`boot -a`) 在启动过程中停止并请求输入。系统会提供一个对话框，在其中显示默认启动值并提供更改它们的选项。您可能希望通过交互式启动来对系统文件或内核进行临时更改。交互式启动允许您测试更改，并在出现问题时轻松恢复。

## 步骤详解

### 交互式启动过程

- 在 `ok` 提示符处，输入 `boot -a` 并按回车。引导程序将交互式地向您提示。
- 根据提示按回车使用默认内核 (`/kernel/unix`)，或输入用于启动的内核名称并按回车。
- 根据提示按回车使用默认模块目录路径，或输入模块目录的路径并按回车。
- 根据提示按回车使用默认的 `/etc/system` 文件。
- 根据提示按回车使用默认的文件系统类型（本地磁盘使用 `ufs`，无盘客户端使用 `nfs`）。
- 按回车使用根设备的默认物理名称。

# 第1章 系统启动与关闭

```
se0 at ebus: offset 14,400000
se0 is /pci1f/pci01/ebus@01/14,400000
cpu: SUNW,UltraSPARC-III (upaid 0 impl 0x2 rev 0x13 clock 270 MHz)
configuring IPv4 interfaces: SUNW,hme0 : PCI IO 2.0 (Rev Id = ci) Found
PCI-device: network01,hme0
hme0 is /pci1f/pci01/network01,1
hme0:
configuring IPv6 interfaces: hme0.
Hostname: unknown
network: unknown: there are no existing databases

wait
meantink: unknown: there are no existing databases

dump on /dev/disk/c0t0ds1 size 42 MB
SUNW,hme0 : Auto-Negotiated 100 Mbps Half-Duplex Link
The system is coming up. Please wait.
checking ufs filesystems
/dev/rdsk/c0t0db5: clean.
/dev/rdsk/c0t0db8: clean.
/dev/rdsk/c0t0db: discovery.
Starting IPv6 neighbor discovery.
Setting default IPv6 interface for multicast: add net ff0::8: gateway
fe08:a000:fea2:6382
starting rpc services: rpc bind.
Setting default IPv4 interface for multicast: add net 224.0.0/4:
syslog service started.
syslog: line 24: WARNING: loghost could not be resolved
Print services started.
Mar 13 11:04:03 unknown pseudo: pseudo-device: todo
Mar 13 11:04:03 unknown genunix: todo is /pseudo/todo
Mar 13 11:04:03 unknown pseudo-device: pm00 is
/pseudo/pm00
Mar 13 11:04:04 unknown simba: pci-device: SUNW,m64B2, m64
Mar 13 11:04:04 unknown genunix: m64 is /pci1f,0/pci01/1/SUNW,m64B2
Mar 13 11:04:04 unknown m64: m64@: 115x200, 44 mappable, rev 475.0: volume management started.
Mar 13 11:04:06 unknown pseudo: pseudo-device: vol0
Mar 13 11:04:06 unknown genunix: vol0 is /pseudo/vol0
Mar 13 11:04:07 unknown scsi: sd0 at uata0: target 2 lun 0
Mar 13 11:04:07 unknown genunix: sd0 is /pci1f,0/pci01,1/ide3/sd2/0
Mar 13 11:04:09 unknown ebus: fd at ebus0: offset 14,3023f0
Mar 13 11:04:09 unknown genunix: fd0 is /pci1f,0/pci01,1/ebus1/fd3@14,3023f0

Mar 13 11:04:15 unknown snmpdx:
The system is ready.
```

ultra console login:

### 第一节 第一部分

如果您不在系统控制台前查看启动信息，可以使用 UNIX 的 `dmesg` 命令重新显示启动过程中显示的信息，或者在 `/var/adm/messages` 文件中查看信息。

### 注意

要查看启动过程中显示的消息，请使用以下方法之一：

- 在 UNIX 提示符下，输入 `/usr/sbin/dmesg` 并按回车。启动消息将显示出来。
- 在 UNIX 提示符下，输入 `more /var/adm/messages` 并按回车。

### 警告

除非您确定结果，否则不要修改 `/etc/system` 文件。良好的做法是对您修改的任何系统文件创建备份副本，以防需要还原，防止系统无法启动。如果 `/etc/system` 文件不可用，请使用交互式选项 `-a` 启动系统。当要求输入系统文件名时，输入备份文件的名称。

## 系统运行状态

`boot` 命令启动内核后，内核将开始启动过程的几个阶段。第一个任务是 OpenBoot 加载内核。如所述，内核是 `/kernel/unix`，位于磁盘上的根 (`/`) 分区，其路径在 OpenBoot PROM 别名中定义。

内核由一个小型核心和许多动态加载的内核模块组成。许多内核模块在启动时自动加载，但为了效率，其他模块（如设备驱动程序）根据内核需要从磁盘加载。当内核加载时，它会读取名为 `/etc/system` 的文件。该文件中的参数控制启动时要加载哪些模块和参数。有时，需要为了性能调优调整此文件中的内核参数。

系统控制权移交给内核后，系统开始初始化并进入表 1.2 描述的八种运行状态之一（也称为 `init`）。由于运行状态 4 是[待定]，运行状态 4 是备用状态。

表 1.2 系统运行状态

| 运行状态 | 描述 |
| :--- | :--- |
| 0 | 自动协商 100 Mbps 半双工链路 |
| 1 | 单用户模式 |
| 2 | 不带 NFS 的多用户模式 |
| 3 | 带有 NFS 的多用户模式 |
| 4 | 备用状态（未使用） |
| 5 | 关机模式 |
| 6 | 重启 |
| 7 | [待定] |
| 8 | [待定] |

### 系统启动与关机

确定启动其他进程的顺序以及当其中一个进程结束时应该做什么。`/etc/inittab` 文件中的每个条目都包含以下字段：

`id:runlevel:action:process`

表 1.4 提供了每个字段的更详细描述。

#### 表 1.4

#### INITTAB 文件中的字段

| 字段 | 说明 |
|---|--|
| id | 唯一标识符 |
| runlevel | 运行级别 (run level) |
| action | 进程运行方式 |
| process | 执行的命令名称 |

以下示例显示了一个默认的 `/etc/inittab` 文件：

```
ap:sysinit/sbin/autopush -f /etc/lu
ap:sysinit/sbin/soconfig -f /etc/scock2path
fs:sysinit/sbin/rc5 sysinit>/dev/msglog 2></dev/msglog </dev/console
is3:initdefault
```

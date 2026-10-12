
udev 进行设备识别的步骤如图 8-5 所示。

![](img/f332344337ca8bf6846cb313a66ee0b3_264_0.png)

*图 8-5 通过热插拔附加新设备的序列*

这些步骤如下：

1. 添加一个新设备，并发生机器检查。
2. 机器检查处理程序通知通用 I/O 层关于新设备的信息。
3. 在通用 I/O 中获取有关所添加设备的信息。在 sysfs 中创建一个新条目。
4. 调用热插拔（Hotplug）。
5. 调用 udev。
6. udev 引用 sysfs。
7. 创建设备文件。

Sysfs 提供用户空间接口以访问内核空间中的数据结构。Sysfs 可以通过热插拔代理和用户操作动态添加和删除。它还允许设置设备与驱动程序的选项（例如日志级别）以及确认设备状态（例如在线或离线）。

Sysfs 包含虚拟配置和控制文件，例如：

- 配置 OSA 设备的示例
  ```
  # echo "0.0.0769,0.0.076a,0.0.076b" > /sys/bus/ccwgroup/drivers/geth/group
  # echo 1 > /sys/bus/ccwgroup/drivers/geth/0.0.0769/online
  ```

- 更改日志级别的示例
  ```
  # echo 2 > /sys/bus/ccw/drivers/zfcp/loglevel_qdio
  ```

- 将通道路径设置为离线/在线的示例
  ```
  # echo offline > /sys/devices/css0/chp0.xx/status
  # echo online > /sys/devices/css0/chp0.xx/status
  ```

- 更改选项设置的示例
  ```
  # echo 1 > /sys/devices/geth/0.0.e18c/layer2
  ```

## 8.2.3 设备驱动程序

以下是 Linux 在 System z 配置中常见的设备驱动程序、其对应的内核模块（如适用）以及描述和特征：

- DASD 设备驱动程序
    - 内核模块：dasd_mod, dasd_eckd_mod, dasd_fba_mod。
    - 用于访问通道附加 DASD 设备的设备驱动程序。
    - 通道子系统处理路径控制和错误恢复。Linux 不考虑路径的存在。
    - Linux 通过使用设备文件 /dev/dasda 进行控制。
        - 第一个分区是 /dev/dasdx1，第二个分区是 /dev/dasdx2。
        - 最大分区数为 3。

- zfcp 设备驱动程序
    - 用于访问通过光纤通道附加的 SCSI 设备的设备驱动程序。
    - 不使用通道子系统。而是使用 QDIO 的缓冲 I/O。因此，Linux 必须自行处理路径控制和错误恢复。
    - 为了识别 LUN，需要主机总线适配器 (HBA) 以及存储服务器侧的逻辑单元号 (LUN) 的信息。
    - Linux 通过使用设备文件 /dev 来识别 LUN。

- 网络设备驱动程序
    - 网络设备由网络设备驱动程序控制。
    - 设备文件和主/次设备号的创建方式与磁盘和磁带相同。
    - 创建接口并将其与设备关联。
    - 接口的默认名称取决于接口类型，例如以太网 (eth0, eth1)，HyperSockets (hsio, hsi)。可以更改接口名称 <geth>。
    - 使用设备驱动程序来访问 QDIO 模式的 OSA-Express 和 HyperSockets。
    - 不使用通道子系统。而是使用 QDIO 的缓冲 I/O。
    - qeth 设备驱动程序需要 3 个子通道才能识别 OSA 设备：
        - 偶数编号的控制读设备。
        - 控制写设备必须是读子通道的设备总线 ID 加一。
        - 数据设备可以是同一 CHPID 上任何空闲的设备总线 ID。

## 8.2.4 确认通道路径和设备状态

本节描述用于确认设备状态的命令和文件。可以确认 sysfs 提供的设备状态。即使在正常情况下，确认状态也很重要。

![](img/f332344337ca8bf6846cb313a66ee0b3_266_0.png)

| 类别 | 命令/文件 | 描述和内容 |
| :--- | :--- | :--- |
| **通用** | `lscss` | 通用 I/O 管理 的设备状态 |
| | `/etc/sysconfig/hardware/*` | 设备信息 |
| **DASD** | `lsdasd` | 关于 DASD 的组成信息 |
| | `/sys/bus/ccw/drivers/dasd-eckd/0.0.<addr>` | 关于 DASD 的组成信息 |
| | `/proc/dasd` | 关于 DASD 的组成信息和统计信息 |
| **FCP** | `lsscsi` | SCSI 设备信息 |
| | `/sys/bus/ccw/drivers/zfcp/0.0.<addr>` | 关于 SCSI 设备的组成信息 |
| | `/proc/scsi/IBMtape, /proc/scsi/IBMchanger` | FCP 磁带设备信息 |
| **网络** | `lsqeth` | 关于 qeth 网络设备的组成信息 |
| | `/sys/bus/ccwgroup/drivers/qeth/0.0.<addr>` | qeth 网络设备信息 |
| | `/proc/qeth` | qeth 网络设备信息 |

可以使用 `lscss` 命令确认通道路径和设备状态。参见示例 8-2。

### 示例 8-2 确认通道路径状态和设备状态

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

### 通道路径状态

使用 `lscss` 命令并查看标记为 PIM、PAM 和 POM 的列来确认物理路径状态。这些是包含在子通道信息块中的路径状态信息的一部分。参见图 8-6。

![](img/f332344337ca8bf6846cb313a66ee0b3_268_0.png)

图 8-6 确认通道路径状态

### 确认设备状态

要确认 DASD 的状态，请使用位于 /proc/dasd/devices 中的 `lsdasd` 命令。

此命令的输出将与示例 8-3 中的输出相似。

#### 示例 8-3 确认 DASD 状态

| 设备 | 类型 | (at) | 卷 | 状态 | 详细信息 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0.0.c128 | (ECKD) | at | (94: 0) | 是 dasda : 活动 | at 块大小 4096, 601020 个块, 2347 MB |
| 0.0.c129 | (ECKD) | at | (94: 4) | 是 dasdb : 活动 | at 块大小 4096, 601020 个块, 2347 MB |
| 0.0.c12a | (ECKD) | at | (94: 8) | 是 dasdc : 活动 | at 块大小 4096, 601020 个块, 2347 MB |

要确认 FCP 设备状态，请使用 `lsscsi` 命令，如示例 8-4 所示。

#### 示例 8-4 确认 FCP 设备状态

```
# lscssi -v
sysfsroot: /sys
[0:0:1:0]      disk      IBM      2105800      .112  /dev/sda
dir: /sys/bus/scsi/devices/0:0:1:0
[/sys/devices/css0/0.0.0007/0.0.f441/host0/0:0:1:0]
```

要确认 OSA 状态，请使用 `lsqeth` 命令（此命令仅适用于 SLES），如示例 8-5 所示。

#### 示例 8-5 lsqeth 命令的输出 - 确认 OSA 设备

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


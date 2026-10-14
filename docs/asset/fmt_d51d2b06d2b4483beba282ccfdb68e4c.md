
| | | 2 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. |/ Log/ |) | | |able (y/n) | (e.g. V.) | (e.g. / |/ |) | |

| | | 2 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 3 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 4 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 5 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 6 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 7 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 8 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 9 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | Drive 3 | 1 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 2 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 3 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 4 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| | | 5 | (e.g. `/dev/hda`) | (e.g. `/dev/hda`) | (e.g. Prim/ Log/Ext) | | Bootable (y/n) | (e.g. Vfat) | (e.g. /usr/home) | |

| 章节 | 对象 | 驱动器设备 (例如`/dev/hda`) | 类型 | 厂商 | 型号 | 主/从 | 访问时间 (ms) | RPMS |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| | | 驱动器 3 | 6 | | | | | |

| | | B | 7 | | | | | |

| | | B | 9 | | | | | |

| 网络 | 互联网服务提供商信息 | | | | | | | |

| | ISP 名称 | | | | | | | | | |

| | 协议 (例如 PPP, SLIP) | | | | | | | | |

| | 电话号码 | | | | | | | | | |

| | 回环接口 (lo) (标准) | | | | | | | 127.0.0.1 | |

| | IP 地址 子掩码 IP 地址 | | | | | | | 255.0.0.0 设备 (例如 COM1 /ttyso) | |

| | 调制解调器厂商 | | | | | | | | |

| | 互联网服务提供商 (ISP) 信息 (调制解调器) 类型 (例如 dhcp, static) | | | | | | | | | |

| | 型号 | | | | | | | | | |

| | 波特率 | | | | | | | | | |

| | IP 地址 | | | | | | | | | |

| | 广播地址 | | | | | | | | | |

| | 网关地址 | | | | | | | | | |

| | 域名服务地址 | | | | | | | | | |

| | IP 地址 | | | | | | | | | |

| | 掩码地址 | | | | | | | | | |

| | 网关地址 | | | | | | | | | |

| | 域名服务地址 | | | | | | | | | |

| | 网卡地址 | | | | | | | | | |

## 附录 B 故障排除 573

我的 SCSI 卡或 Zip 驱动器没有被系统识别。我需要指定哪些参数，以及如何指定它们才能使其正常工作？

这个问题与上一个问题有关。如果 TurboLinux 没有检测到你的 SCSI 卡，你将需要帮助它。首先，你必须知道你的 SCSI 卡的品牌和型号。你可能还需要知道该 SCSI 卡使用的是什么芯片组。完成后，请参考上一节提到的 BootPrompt HOWTO 网站，以找到该型号/芯片组的内核选项。

如果你有一个 SCSI Zip 驱动器，当 Linux 正确识别你的 SCSI 卡时，你应该能够像使用系统中其他驱动器一样使用该驱动器。如果你使用的是预格式化的 Zip 磁盘，你需要指定 `/dev/sda4`，因为预格式化的 Zip 磁盘使用第四个分区。

### LILO 安装失败。我该如何恢复？

如果遵循了配置 LILO 的所有步骤，LILO很少失败。尽管如此，意外仍然会发生，有时硬件错误会导致你的系统 LILO 失败。

当 LILO 启动时，你通常会看到 LILO 指示。如果 LILO 发生错误，你会看到 LILO 的子集，例如 "LIL"LI"LIL" 和 "LILO"。最常见且可修复的问题导致显示 "LIL" 或 "LILO"。这通常表示你需要更改内核或 `/etc/lilo.conf` 配置，并运行 LILO 将更改写入到 LILO 安装的位置——即 MBR，或者从你的系统软盘磁盘重新安装并运行 `lilo` 命令。如果你没有系统引导软盘，可以使用其他方法（例如 Linux 救援急盘）从软盘启动一个最小的 Linux 系统。然后，挂载你的 Linux 文件系统并使用适当的参数运行 `lilo`，以让 LILO 写入 MBR。

由于这可能有点复杂，你可能会发现直接从你的内核镜像创建一个系统软盘，比尝试让 LILO 从救援急盘的环境中写出信息要简单。请参考第 4 章“安装后操作”，学习如何制作系统软盘。

### 我在安装中途崩溃了。我该如何找到并设置缺失的信息？

首先，这不应该发生。然而，如果你发现 TurboLinux 安装过程中的 bug 导致安装失败，你的操作将取决于安装是在哪个阶段失败的。

如果在所有软件软件包都安装之前安装失败，你必须向 http://www.turbolux.com/support/bug.html 的 TurboLinux bug 跟踪系统报告该 bug，并可以尝试重新安装，避免你可能导致失败的选项。

## 附录

如果在所有软件包安装后安装失败并提示你输入 root 密码。你应该能够登录系统并使用 `turntools-turbofscfg`、`turbonnetcfg`、`turboprintcfg`、`turboser-vice`、`turbotimecfg`、`turbousercfg` 等配置剩余的项目。

你可以在 `/tmp/turbopkg.log` 中找到安装日志，有助于你确定安装在哪里停止的。请务必发送日志以及失败安装留下的任何核心文件。

## 互联网和网络连接

我的电脑无法连接互联网。我现在该怎么办？

该解决方案取决于你尝试如何连接互联网。

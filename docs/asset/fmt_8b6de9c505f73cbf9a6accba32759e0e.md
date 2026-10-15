
| ATA/IDE/MFM/RLL support | Large collection of options to configure the kernel to communicate using different types of data communication protocols to talk to mass storage devices, such as hard drives. Note that this section does not cover SCSI. |
| SCSI device support | Options for configuring the kernel to support Small Computer System Interface. This subsection covers drivers for specific cards, chipsets, and tunable parameters for the SCSI protocol. |
| Old CD-ROM drivers | Configuration options to support obscure older CD-ROM devices that do not conform to the SCSI or IDE standards. These are typically older CD-ROM drivers that are usually a proprietary type of SCSI (not SCSI, not IDE). |
| Multi-device support | Options for enabling the kernel to support RAID devices in (RAID and LVM) software emulation and the different levels of RAID. Also contains options for support of a logical volume manager. |
| Fusion MPT device support | Configures support for LSI's Logic Fusion Message Passing Technology. This technology is for high performance SCSI and local area network interfaces. |
| IEEE1394 (firewire) support | Experimental support for Firewire devices. |

## 表 32.1 配置的内核子部分

| 名称 | 描述 |
|---|---|
| I2O 设备支持 | 用于支持智能输入/输出架构的选项。此架构使硬件驱动程序能够与操作系统驱动程序分离，从而使大量硬件设备能够在一个实现中与操作系统兼容。 |
| 网络支持 | 内核中网络配置的多个选项。选项用于支持的协议类型以及这些协议的可配置选项。 |
| 业余无线电支持 | 用于配置支持 AX25 协议的设备的选项。 |
| IrDA（红外）支持 | 用于配置红外数据协会协议套件以及使用这些协议的设备的选项。 |
| Bluetooth 支持 | 对 Bluetooth 无线协议的支持。包括支持 Bluetooth 协议和硬件设备的选项。 |
| ISDN 子系统 | 用于支持综合业务数字网协议和设备的选项。ISDN 是一种通过经过调制的电话线以数字方式连接到广域网的方法，主要用于将用户连接到 ISP。 |
| 电话支持 | 对能够使用普通电话线路支持 VoIP 应用的设备的支持。本节不处理调制解调器的配置。 |
| 输入设备支持 | 用于配置通用串行总线（USB）人机接口设备（HID）的选项。这些包括键盘、鼠标和操纵杆。 |
| 字符设备 | 用于与服务器以顺序字符通信的设备的配置选项。这是一个包含多个主板芯片组驱动程序的大型子部分。 |
| 多媒体设备 | 视频和声音设备的硬件实现的驱动程序，例如视频采集板、电视卡和 AM/FM 收音机适配器卡。 |
| 图形支持 | 配置 VGA 文本控制台、视频模式选择以及帧缓冲卡的支持。 |
| 声音 | 用于配置支持的声卡驱动程序和内核的芯片组支持的大型子部分。 |
| USB 支持 | 通用串行总线配置选项。包括对 USB 设备的配置，以及 USB 的厂商特定版本。 |
| 文件系统 | 用于支持的文件系统类型的配置选项。 |
| 附加设备驱动程序支持 | 用于第三方补丁的部分。 |
| 配置文件支持 | 对内核行为进行分析以帮助调试和开发。 |
| 内核 Hacking | 本节确定内核是否将包含高级调试选项。大多数用户不希望在其生产内核中包含此选项，因为它会增加内核大小并通过添加额外例程来降低性能。 |
| 安全选项 | 确定是否启用 NSA 安全增强型 Linux（SELinux）。 |
| 加密选项 | 对加密硬件的支持（Ubuntu 补丁在“原版”内核源代码中未找到）。 |
| 库例程 | 包含 zlib 压缩支持。 |

在选择完所有想要的选项后，您可以保存配置文件并继续执行内核编译清单中所示的第 7 步。

## 创建初始 RAM 磁盘映像

如果您需要加载特殊的设备驱动程序才能挂载根文件系统（例如 SCSI 驱动器、网卡或奇特的文件系统），则必须创建一个名为 `/boot/initrd.img` 的初始 RAM 磁盘映像。对于大多数用户来说，创建此文件不是必需的，但如果您不确定，创建它也不会有什么坏处。要创建 `initrd.img` 文件，请使用 shell 脚本 `/sbin/mkinitrd`。

命令的格式如下：

```
/sbin/mkinitrd file_name kernel_version
```

其中 `file_name` 是您想要创建的映像文件的名称。

`mkinitrd` 会查看 `/etc/fstab`、` /etc/modprobe.conf` 和 `/etc/raidtab` 以获取其所需的信息来确定在启动期间应加载哪些模块。对于我们的系统，我们使用

```
# mkinitrd initrd-2.6.7-1.img 2.6.7-1
```

## 出现问题时

在内核编译和安装过程中可能会出现多种问题，而多种线索会指向真正的问题。你会在屏幕上看到错误信息，部分错误信息也会打印到文件 `/var/log/messages` 中，可用文本编辑器查看。如果你已按照我们的说明对内核进行过补丁，还需要检查一个特殊的错误日志。不要担心错误，因为许多问题都可以通过你自己的研究轻松解决。然而，某些错误可能无法修复，这取决于你的技能水平和技术信息的可用性。

### 编译期间的错误

虽然内核无法编译的情况很少见，但总是有可能在回归测试中出现疏漏。让我们看一个编译过程中可能出现问题的示例。

内核编译可能会崩溃并无法成功完成，尤其是在你尝试使用实验性补丁、添加未经测试的功能，或在旧系统上构建更新且可能不稳定的模块时。

此时，你有两个选择：

- 修复错误并重新编译。
- 删除有问题的模块或选项，等待内核团队修复错误。

大多数用户由于内核代码的复杂性而无法修复某些错误，尽管不应排除此选项。可能其他人在内核测试期间发现了相同的错误并为该问题开发了补丁：请查看 Linux 内核邮件列表存档。如果问题在那里没有提及，在 Google 上搜索可能会找到相关信息。

第二个选项，即删除代码，是最简单的方法，也是大多数人在有问题的代码不是必需的情况下所做的。在 NTFS 模块失败的情况下，这几乎是意料之中的，因为 NTFS 支持仍被视为实验性且容易出错。这主要是因为文件系统的代码是通过逆向工程实现的，而不是通过记录的标准实现。只读支持在最近的内核中有所改善；写支持仍然是实验性的。

最后，如果你想尝试自己解决这个问题，这是一个参与 Linux 内核并做出贡献、帮助他人的绝佳机会。

如果你对编码和内核事务有所了解，可以查看内核源代码中 `/usr/src/linux-2.6/` 目录下的 `MAINTAINERS` 文件，找到该代码的维护者。建议的做法是联系维护者，看看他是否知道你遇到的问题。如果没有针对特定错误进行记录，将错误提交到内核邮件列表是一个选项。执行此操作的指南在内核源代码根目录下的 `README` 文件中，在“如果出现问题”部分。

### 运行时错误、引导加载程序问题和内核 Oops

运行时错误发生在内核加载时。错误信息会显示在屏幕上或写入 `/var/log/messages` 文件。引导加载程序问题会将信息显示在屏幕上；不会产生日志文件。内核 Oops 是运行中内核的错误，错误信息会写入 `/var/log/messages` 文件。

互联网上存在大量优秀的文档，可用于排查 LILO、GRUB 或内核在启动期间可能出现的几乎所有类型的错误。找到这些文档的最佳方法是前往你喜欢的搜索引擎，输入你收到的错误的关键词。你需要根据搜索的聚焦程度调整使用的关键词。

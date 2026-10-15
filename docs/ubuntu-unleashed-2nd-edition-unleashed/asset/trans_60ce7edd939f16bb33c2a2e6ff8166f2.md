

| Name | Description |
|---|---|
| Code maturity level options | 允许将开发代码编译到内核中，即使该代码已被标记为已废弃或仅为测试代码。此选项仅应由内核开发者或测试人员使用，因为在开发过程中代码可能处于不可用状态。 |
| General setup | 本节包含多个不同的选项，涵盖内核如何与 BIOS 通信，是否应支持 PCI 或 PCMCIA，是否应使用 APM 或 ACPI，以及将支持何种 Linux 二进制格式。包含用于支持运行为其他系统编译的二进制文件而无需重新编译程序所需的内核结构的多个选项。 |
| Loadable module support | 确定内核是否启用驱动程序和其他非必要代码作为可加载模块进行编译，以便在运行时加载和卸载。此选项可保持基本内核精简，从而能够更快地运行和响应；因此，选择此选项通常是一个好主意。 |
| Processor type and features | 与将运行内核的架构相关的多个选项。 |
| Power management options | 与 ACPI 和 APM 电源管理功能相关的选项。 |
| Bus options | 用于笔记本电脑中 PCMCIA 总线和 PCI 热插拔设备的配置选项。 |
| Memory Technology Devices (MTD) | 用于支持闪存设备（如 EEPROM）的选项。通常，这些设备用于嵌入式系统。 |
| Parallel port support | 用于配置内核如何支持并行端口通信的多个选项。 |
| Plug-and-play configuration | 用于支持即插即用 PCI、ISA 和即插即用 BIOS 支持的选项。通常，最好为 PCI 和 ISA 设备支持即插即用。 |
| Block devices | 处理以字符块而非流的方式与内核通信的设备的部分。这包括通过并行端口连接的 IDE 和 ATAPI 设备，以及启用网络设备作为块设备进行通信。 |
| ATA/IDE/MFM/RLL support | 用于配置内核使用不同类型的数据通信协议与大容量存储设备（如硬盘）通信的大量选项。请注意，本节不涵盖 SCSI。 |

## 表 35.1 继续

| Name | Description |
|---|---|
| SCSI device support | 用于配置内核以支持小型计算机系统接口的选项。本小节涵盖特定卡、芯片组以及 SCSI 协议的可调参数的驱动程序。 |
| Old CD-ROM drivers | 用于支持不符合 SCSI 或 IDE 标准的晦涩、旧式 CD-ROM 设备的配置选项。这些通常是通常为专有类型的 SCSI（非 SCSI，非 IDE）的旧式 CD-ROM 驱动程序。 |
| Multi-device support | 用于启用内核支持 RAID 设备在（RAID 和 LVM）软件仿真中以及不同级别的 RAID 的选项。也包含对逻辑卷管理器支持的选项。 |
| Fusion MPT device support | 配置对 LSI Logic Fusion 消息传递技术的支持。该技术用于高性能 SCSI 和局域网接口。 |
| IEEE1394 (firewire) support | 对 Firewire 设备的实验性支持。 |
| I2O device support | 用于支持智能输入/输出架构的选项。该架构使硬件驱动程序能够与操作系统驱动程序分离，从而使多种硬件设备能够在一个实现中与操作系统兼容。 |
| Networking support | 内核中网络配置的多个选项。选项包括支持的协议类型以及这些协议的可配置选项。 |
| Amateur radio support | 用于配置支持 AX25 协议的设备的选项。 |
| IrDA (infrared) support | 用于配置支持红外数据协会协议套件以及使用这些协议的设备的选项。 |
| Bluetooth support | 对蓝牙无线协议的支持。包括支持蓝牙协议和硬件设备的选项。 |
| ISDN subsystem | 用于支持综合业务数字网络协议和设备的选项。ISDN 是一种通过调制电话线路以数字方式连接到广域网的方法，主要用于将用户连接到 ISP。 |
| Telephony support | 对启用使用普通电话线路支持 VoIP 应用的设备的支持。本节不处理调制解调器的配置。 |
| Input device support | 用于配置通用串行总线（USB）人机接口设备（HID）的选项。这些包括键盘、鼠标和操纵杆。 |
| Character devices | 用于与服务器以顺序字符通信的设备的配置选项。这是一个包含多个主板芯片组驱动程序的大型小节。 |


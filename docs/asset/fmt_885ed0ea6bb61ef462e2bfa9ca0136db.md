
# 第 3 章：特殊硬件与电源管理

## 探索电源管理选项

```
OPTIONS=-s /var/run/acpid.socket"
```

还有针对 `MODULES` 指令的选项。第一个指定了要加载的模块列表；第二个则没有限制。这两个指令中的第一个用井号（`#`）“注释掉”了。你也可以使用井号来禁用第二个指令。不要在同时激活两个指令的情况下保存文件，因为它们无法共同工作。

```
#MODULES="battery ac processor button thermal"

MODULES="all"
```

为了进行故障排除，还有一个 `acpi_listen` 命令。在命令行中运行时，它看起来像挂挂了——但实际上正在监听与 ACPI 相关的电源事件。如果你正在运行笔记本系统，连接或断开系统的 ACPI 电源可能会导致此处所示的事件：

```
ac_adapter 00000080 00000000
```

笔记本系统上的热键通常与笔记本的电源管理功能最相关。

问题之一是不同的笔记本电脑和主板配置了不同的电源事件。查看可用电源事件的一种方法是查看从 `acpi-support` 包安装的文件列表。在命令行中，你可以使用以下命令查看此列表（如果已安装该包）：

```
$ dpkg -L acpi-support
```

许多为 ACPI 配置的文件是特定厂商的；考虑到近期所有权的变更（例如联想收购了 IBM PC 部门，以及酷尔收购了 Gateway），在读取这些文件名时需要一定的灵活性。

读取几个单独笔记本事件。你会发现一些通用的厂商无关脚本。例如，`ibm-sleepptn`、`panasonic-sleepptn` 和 `sony-sleep` 所有事件都指向了 `/acpi` 目录下的 `sleepn.sh`。

键码 e009 是用户在 Dell 笔记本电脑系统上同时按下 FUNCTION 和 F10 键时接收到的信号。它映射到 `KEY_EJECTCD` 变量，该变量也可以 `/etc/acpi/eventbtn.sh` 中找到。

基础配置由 `setkeys` 命令驱动。它以十六进制表示映射笔记本电脑键盘上的按键，并根据变量触发相应的事件。默认键码存储在同一目录下的 `atkbd.hk` 文件中。它列出了所有标准键位映射，例如字母 F 映射到键码 21。许多标准键码在该文件中被“预留”出来，以便通过其他文件进行自定义定制。

| 类别 | 热键设置文件 | 描述 |
|---|---|---|
| `/etc/acpi/events` 下的 ACPI 事件文件 | `acer-asper-1600.hk` | 为 Acer Asper 1600 系列笔记本电脑设置热键 |
|  | `acer.hk` | 关联其他 Acer 笔记本电脑的热键 |
|  | `asus.hk` | 为华硕笔记本电脑分配热键 |
|  | `atkbd.hk` | 设置键盘的默认值 |
|  | `clevo-dp500p.hk` | 为 Clevo 的 Keyux Agora 系统关联键码 |
|  | `compaq.hk` | 为 Compaq 系统（现由 HP 销售）配置按 |
|  | `default.hk` | 列出未由其他文件配置的笔记本键 |
|  | `dell.hk` | 为 Dell 笔记本电脑配置特殊键，包括多媒体直接键 |
|  | `generic.hk` | 列出所有笔记本通用的键码 |
|  | `hp.hk` | 为 HP 系统设置热键 |
|  | `hp-tablet.hk` | 为 HP 平板系统设置热键；另见 `hp.hk` 和 `compaq.hk` |
|  | `hp-v2000.hk` | 配置与 Compaq 最初开发的 Presario 笔记本型号相关的热键 |
|  | `ibm.hk` | 为各种 Thinkpad 和联想笔记本电脑关联高度自定义的键码 |
|  | `key-constraints` | 为标准键设置变量，例如 `KEY_ESC=1` |
|  | `lenovo.hk` | 为联想系列笔记本电脑关联自定义键码 |
|  | `medion.hk` | 为 Medion 笔记本电脑配置自定义键码 |
|  | `micro-star-infinity.hk` | 为 MSI MS-1035 笔记本系统设置热键 |
|  | `samsung.hk` | 为三星系统设置热键 |
|  | `tohiba-table.hk` | 配置 Toshiba Portage 平板的热键 |

## 复习特殊硬件问题

### 认证目标 3.03

正如 Linux ACPI 系统为不同的笔记本制造商包含自定义键码信号配置一样，系统还包含了针对不同硬件的许多自定义配置。`smartmontools` 包可以监控连接硬盘的健康状况。串接口（SATA）硬盘在某些方面模拟 SCSI 硬盘。ACPI 状态与电源模式相关。直接内存访问（DMA）允许各个硬件系统绕过 CPU。无线设备一直是 Linux 面临的一个特殊挑战。通过蓝牙和红外设备，更多挑战得到了克服。

## 智能硬盘监控

当前版本的 Ubuntu Linux 包含基于 `smartmontools` 包的硬盘监控器。目前，它主要关注本地硬盘的健康状况，这是基于内置在 SATA、SCSI 以及后期型号 IDE 硬盘中的自监控、分析和报告技术（SMART）系统。Ubuntu 该文件的默认版本仅包含默认设置。关键命令是 `smartctl`。这是一个正确的命令。

虽然监控可以在 `/etc/default/smartmontools` 文件中进行配置，但理解每一个开关已超出 UCP 考试的范围。你应该了解基础知识；例如，以下命令列出了第一块 SATA（或 SCSI）硬盘上的所有 SMART 报告信息。输出到分页符的“管道”（pipes）越少（`less` 命令越少），这在 UCP 专家水平上应该已经知道了。

```
$ sudo smartctl -a /dev/sda | less
```

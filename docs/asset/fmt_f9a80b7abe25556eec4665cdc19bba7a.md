
| name | 一个文本字符串，理想情况下具有一定的助记价值（例如，`sd` 代表“SCSI 磁盘”）。许多名称，尤其是即插模块的名称，包括设备制造商的名称或股票代码（例如，`SUNW` 是 Sun Microsystems 的股票代码）。 |

| `@` | 将名称与地址参数分隔开。 |

| address | 表示地址的文本字符串，通常形式为 `hex_number,hex_number`。（数字以十六进制格式给出。） |

| `:` | 必须位于参数的参数之前。 |

| arguments | 格式取决于特定设备的文本字符串。可用于向设备的软件传递信息。 |

OpenBoot 命令需要完整的设备路径名来定位并区分不同的设备。这意味着您可以毫无歧义地指定特定设备。

示例：

`/sbus@1,f8000000/esp@0,40000/sd@3,0:a`

`1,f8000000` 表示主系统总线上的地址，因为 SBus 接口直接连接到主系统总线。

`0,40000` 是 SBus 插槽号。`esp` 设备位于 SBus 插槽 0，偏移量为 `40000`。（在此示例中，该设备是 SCSI 主机适配器，尽管名称并未直接说明。）

`3,0` 是 SCSI 目标和逻辑单元号。`sd` 设备连接到 SCSI 总线，目标为 3，逻辑单元为 0。

有关 SCSI 主机适配器、目标和逻辑单元的更多信息，请参阅附录 C，“SCSI 设备概述”。

节点名称中的 `:arguments` 部分是可选的。在前面的示例中，`sd` 设备的参数是字符串 `a`。Solaris 软件驱动程序将 `sd` 的参数解释为磁盘分区，因此设备路径名指的是该磁盘上的分区 `a`。

### PROM 设备别名

OpenBoot 识别两种类型的设备路径名：

- 完整设备（在上一节中讨论过），例如 `/sbus@1,f8000000/esp@0,40000/sd@3,0:a`
- 设备别名，例如 `disk`

别名是长设备路径名的简写。别名代表整个设备路径名，而不是其组成部分。例如，别名 `disk` 可能代表设备路径名

`/sbus@1,f8000000/esp@0,40000/sd@3,0:a`

OpenBoot 为常用设备提供了以下预定义设备别名，因此您很少需要输入完整的设备路径名。

| 别名 | 设备路径名 |
|---|---|
| disk | /sbus@1,f8000000/esp@0,40000/sd@3,0:a |
| disk1 | /sbus@1,f8000000/esp@0,40000/sd@1,0:a |
| disk2 | /sbus@1,f8000000/esp@0,40000/sd@2,0:a |
| disk3 | /sbus@1,f8000000/esp@0,40000/sd@3,0:a |

表 1-3 描述了 `devalias` 命令，该命令用于在 OpenBoot 中检查、创建和更改别名。

#### 表 1-3 devalias 示例

| 命令 | 描述 |
|---|---|
| devalias | 显示所有当前设备别名。 |
| devalias alias | 显示与别名对应的设备路径名。 |
| devalias alias device-path | 定义代表设备路径的别名。 |

### 在 OpenBoot 中获取帮助

每当在显示屏上看到 `ok` 提示符时，您可以通过输入表 1-4 中描述的帮助命令之一向系统请求帮助。

#### 表 1-4 帮助命令

| 命令 | 描述 |
|---|---|
| help | 显示有关使用帮助系统的说明并列出可用的帮助类别。 |
| help category | 显示该类别中所有命令的帮助。仅使用类别描述的第一个词。 |
| help command | 显示单个命令的帮助。 |

由于命令数量众多，`help` 仅适用于经常使用的命令。

例如，如果您想查看类别 `diag` 中所有命令的帮助消息，请键入

```
ok help diag
```

Help 的响应为

```
ok help diag
Category: Diag
test device-specifier (...) run selftest method for specified device
examples:
test /memory -test memory
test /iommu/sbus/ledma@f,400010/le -test net
test floppy -test floppy disk drive
```

```
test net      - test net
test scsi     - test scsi
watch-clock (..)  show ticks of real-time clock
watch-net (..)    monitor broadcast packets using auto-selected interface
watch-aui (..)    monitor broadcast packets using AUI interface
watch-net-all (..) monitor broadcast packets on all net interfaces
probe-scsi (..)   show attached SCSI devices
probe-scsi-all (..) show attached SCSI devices for all host adapters
test-all (..)     execute test for all devices with selftest method
test-memory (..)  test all memory if diag-switch? is true, otherwise test memory specified by selftest-#mgs
ok
```

如果您想要特定命令的帮助，请键入

```
ok help test net
```

Help 响应如下：

```
Category: Diag
test device-specifier (..) run selftest method for specified device
examples:
test /memory          -test memory
test /iommu/sbus/ledma@f,400010/le -test net
test floppy           -test floppy disk drive
test net              -test net
test scsi             -test scsi
```

该消息还显示命令的格式。

### 测试和启动系统

OpenBoot 中最常用的命令是验证系统硬件的命令和启动操作系统的命令。系统电源打开后，会出现 `ok` 提示符，表示系统已准备好接收您的输入。

#### 测试硬件

用于检查系统所有主要组件的 OpenBoot 诊断命令是

```
ok testall
```

系统响应为

```
Target 1
  Unit 0    Disk    SEAGATE ST1120N    833400093849
            Copyright © 1992 Seagate
            All rights reserved 0000

Target 3
  Unit 0    Disk    MAXTOR LXT-213S SUN2074.20
```

`probe-scsi` 检查所有 SCSI 设备的连接性。如果设备未正确连接或共享相同的目标 ID，则设备将无法被识别。

> 提示。使用 `probe-scsi` 命令在添加磁带机、CD-ROM 驱动器、磁盘驱动器或任何其他 SCSI 外设之前获取一个空闲的 SCSI 目标 ID 号。在安装 SCSI 设备后使用此命令，以确保其已正确连接且系统可以识别它。如果怀疑电缆或连接有故障，也请使用此命令。

### 内核初始化阶段

如果 OpenBoot 参数 `auto-boot` 设置为 `true`（默认值）且 OpenBoot PROM 不处于完全安全模式，则 OpenBoot PROM 会自动发出 `boot` 命令。系统在电源打开后自动开始启动过程，您将看不到 `ok` 提示符的显示。要中断自动启动过程，请按 `Stop-A`。`ok` 提示符出现。表 1-5 列出了 `boot` 命令选项。

#### 表 1-5 boot 命令选项

| 选项 | 描述 |
|--------|-------------|
| -a | 交互式启动 |
| -s | 启动到单用户状态 |
| -r | 重新配置 |
| -v | 以详细模式启动 |

例如，`ok boot -v` 以详细模式启动系统，在启动阶段会显示系统消息的完整列表。

`boot` 程序负责将 UNIX 内核加载到内存中并将系统控制权传递给它。内核（本章后面会详细介绍）是操作系统的一部分，在系统关闭之前始终保持运行。

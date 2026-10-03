
任何用户都可以通过在 UNIX 提示符下输入以下命令来查看 OpenBoot 配置变量：

```
/usr/sbin/eeprom
```

例如，要从命令行更改 OpenBoot 参数 security-password，必须以 root 身份登录并发出以下命令：

```
example# eeprom security-password=
Changing PROM password:
New password:
Retype new password:
```

您分配的安全密码必须在零到八个字符之间。第八个字符之后的任何字符都会被忽略。您无需重置系统；安全功能在您键入命令后立即生效。

如果不带参数，eeprom 命令将显示所有 OpenBoot 配置设置，类似于 OpenBoot printenv 命令。

表 2.9 中列出的 NVRAM 命令可用于修改 devalias，使其在重新启动后仍然保持永久有效。

## NVRAM 命令

表 2.9

| 命令 | 描述 |
|---|---|
| nvalias alias device-path | 在 NVRAMRC 中存储命令 devalias alias device-path。（别名会一直保留，直到执行 nvunalias 或 set-defaults 命令为止。）打开 use-nvramrc？ |
| nvunalias alias | 从 NVRAMRC 中删除相应的别名。 |

例如，要永久创建一个名为 disk3 的 devalias，该别名将代表 SPARCstation10 系统上目标 ID 为 3 的 SCSI 磁盘，请键入以下内容：

```
nvalias disk3/iommu/sbus/espdma@f,400000/esp@f,800000/sd@3,0
```

> 警告
设置安全模式和密码可能会导致系统在忘记密码时无法启动。无法在不将 CPU 送往 Sun 进行 PROM 重置的情况下入侵。OpenBoot 安全将在下一节中详细介绍。

> 注
如果您在 SPARC 系统上更改了 NVRAM 设置并且系统不再启动，可以通过在机器加电时同时按住 Stop+N 键将 NVRAM 变量重置为其默认设置。发出此命令时，请在打开 SPARC 系统电源后立即按住 Stop+N；保持这些键按下几秒钟或直到看到横幅（如果显示可用）。这是一种将系统的 NVRAM 变量强制为已知状态的好方法。

## nvedit

在 PROM 版本为 1.x 或 2.x 的系统上，nvalias 命令可能不可用。在这些系统上，您需要使用 nvedit 命令创建自定义设备别名。nvedit 是一个行编辑器，直接编辑 NVRAMRC，具有一组编辑命令，并在临时缓冲区中操作。以下是一个 nvedit 会话示例：

```
ok setenv use-nvramrc? true
```

系统作出如下响应：

```
use-nvramrc? =    true
ok nvedit
0: devalias pgx24 /pci@1f,0/pci@1,1/SUNW,m64B
1: devalias disk0 /pci@1f,0/pci@1,1/ide@3/disk@0,0
2: <Control-C>
ok nvstore
ok reset
  Resetting .....
ok boot disk0
```

在之前的会话中，我使用 nvedit 创建了一个名为 disk0 的永久设备别名。我使用 <control-C> 退出编辑器。我使用 nvstore 命令使更改在 NVRAMRC 中永久生效。我发出 reset 命令重置系统，然后使用 boot disk0 命令从 disk0 启动系统。

表 2.10 列出了在 nvedit 行编辑器中可以使用的一组基本命令。

### nvedit 命令

表 2.10

| 命令 | 含义 |
|---|---|
| control+c | 退出编辑器 |
| control+u | 删除当前行 |
| delete | 删除前一个字符 |
| return | 关闭当前行并打开新行 |
| control+b | 向后移动一个字符 |
| control+f | 向前移动一个字符 |
| control+p | 向上移动一行 |
| control+n | 向下移动一行 |

## OpenBoot 安全

任何有权访问计算机键盘的人都可以访问 OpenBoot 并修改参数，除非您设置了安全变量。这些变量列在表 2.11 中。

### OpenBoot 安全变量

表 2.11

| 变量 | 描述 |
|---|---|
| security-mode | 限制用户在 OpenBoot 提示符下允许执行的操作集。 |
| security-password | 固件安全密码。（它永远不会显示。）请勿直接设置此变量。此变量使用 password 设置。 |
| security-#badlogins | 错误的安全密码尝试次数。 |

> 警告
记住您的安全密码非常重要，并且在设置安全模式之前先设置安全密码。如果您忘记此密码，则无法使用系统；您必须联系供应商的客户支持服务以使机器重新可启动。

要在 ok 提示符下设置安全密码，请键入以下内容：

```
ok password
ok New password (only first 8 chars are used): <enter password>
ok Retype new password: <enter password>
```

之前，我展示了如何从命令行更改 OpenBoot 参数 security-password。

分配密码后，您可以设置最适合您环境的安全变量。

security-mode 用于限制 OpenBoot 命令的使用。当您分配表 2.12 中显示的三个值之一时，对命令的访问会受到密码保护。设置 security-mode 的语法如下：

```
setenv security-mode <value>
```

您为 security-mode 输入的值是表 2.12 中列出的三个值之一。

### OpenBoot 安全值

表 2.12

| 值 | 描述 |
|-------|-------------|
| full | 除 go 之外的所有 OpenBoot 命令都需要密码。此安全模式是最严格的。 |
| command | 除 boot 和 go 之外的所有 OpenBoot 命令都需要密码。 |
| none | 不需要密码（默认）。 |

以下示例将 OpenBoot 环境设置为除 boot 和 go 之外的所有命令都需要密码：

```
setenv security-mode command
```

将 security-mode 设置为 command 时，如果单独键入 boot 命令或键入 go 命令，则不需要密码。任何其他命令都需要密码，包括带参数的 boot 命令。

以下是 security-mode 设置为 command 时可能需要密码的示例：

- `ok boot`  不需要密码。
- `ok go`  不需要密码。
- `ok boot vmunix`  需要密码。

系统按如下方式显示密码提示：

- `Password`  密码在键入时不会回显。
- `ok reset-all`  需要密码。

系统按如下方式显示密码提示：

| 密码 | 输入密码。 |
|---|---|
| 注 | 密码在键入时不会回显。 |

如果您输入了错误的安全密码，在下一个启动提示出现之前大约会有 10 秒的延迟。错误的安全密码可以输入的次数存储在 security-#badlogins 变量中。语法如下：

```
setenv security-#badlogins <variable>
```

例如，您可以使用以下命令将尝试次数设置为四次：

```
setenv security-#badlogins 4
```

## OpenBoot 诊断

可以在 OpenBoot 中运行各种硬件诊断。这些可用于排除硬件和网络问题的故障。这些诊断命令列在表 2.13 中。

### OpenBoot 诊断

表 2.13

| 命令 | 描述 |
|---|---|
| probe-scsi | 识别连接到 SCSI 总线的设备。 |
| probe-ide | 识别连接到 PCI 总线的 IDE 设备。 |
| test device-specifier | 执行指定设备的自检方法。例如：test floppy 测试软盘驱动器（如果已安装）。test net 测试网络连接。 |
| test-all [device-specifier] | 测试指定设备树节点下具有内置自检方法的所有设备。如果未指定 device-specifier，则从根节点开始测试所有设备。 |
| watch-clock | 测试时钟功能。 |
| watch-net | 监视网络连接。 |

使用 probe-scsi 命令在添加磁带机、CD-ROM 驱动器、磁盘驱动器或任何其他 SCSI 外设之前获取空闲的开放 SCSI 目标 ID 号。只有已通电的设备才会被找到，因此请确保所有设备都已打开。在安装 SCSI 设备后使用此命令，以确保其已正确连接并且系统可以看到它。如果怀疑电缆或连接有故障，也请使用此命令。如果有多个 SCSI 总线，请使用 probe-scsi-all 命令。

以下示例使用 OpenBoot 的一些诊断功能。第一个示例使用 probe-scsi 识别连接到特定 SCSI 总线的所有 SCSI 设备。此命令对于识别已使用的 SCSI 目标 ID 或检查所有设备是否已连接并被系统识别很有用。

```
ok probe-scsi
```

系统将作出如下响应：

```
Target 1
    Unit 0  Disk      SEAGATE ST1120N 833400093849
    Copyright   1992 Seagate
    All rights reserved 0000
Target 3
    Unit 0  Disk  MAXTOR LXT-213S SUN2074.20
```

此示例使用 probe-ide 命令识别连接到 PCI 总线的所有 IDE 设备：

```
ok probe-ide
    Device 0 ( Primary Master )
        ATA Model: ST34321A
    Device 1 ( Primary Slave )
        Not Present
    Device 2 ( Secondary Master )
        Removable ATAPI Model: CRD-8322B
    Device 3 ( Secondary Slave )
        Not Present
```

下一个示例测试系统视频并执行其他各种测试：

```
ok test all
```

要测试磁盘驱动器是否正常工作，请将一张已格式化的高密度磁盘放入驱动器中并键入以下内容：

```
ok test floppy
```

系统应作出如下响应：

```
Testing floppy disk system. A formatted disk should be in the drive.
Test succeeded.
```

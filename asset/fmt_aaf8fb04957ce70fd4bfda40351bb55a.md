
停滞在硬盘上。理想情况下，Knoppix 会识别 PC 上的硬件，但在某些情况下，Knoppix CD-ROM 无法识别每一个设备。这并不是致命问题；Knoppix 的启动程序允许你传递“作弊代码”，告诉 Knoppix 和其他文件系统 CD-ROM 发行版如何处理特定硬件。关于此选项的更多信息请参见附录 D。然而，Knoppix 最好的特性是可携性和非侵入性。如图 4.5 所示，任何延迟系统信息都存储在 RAM 中，并在重启时被销。

## Live Linux CD ROM 如何工作

![](img/72e1c6125676a623b5032cfdab8d797c_90_0.png)

- **Live 文件系统 CD ROM**：Linux 安装被复制到带有压缩根文件系统的 CD ROM 中。CD ROM 包含未解压缩的程序文件。书中附的 Knoppix CD 是只读的。这种方式的文件使用的工具和特定应用程序因发行版而异。

- **CD ROM 驱动器**：从 PC 的 CD 驱动器读取 CD ROM。CD ROM 类似于硬盘，尽管 Linux 只能读取文件并写入临时文件。操作系统使用这些文件进行简便的解压缩。这导致 Linux 运行就像是在带有硬盘的同一台 PC 上运行一样。

- **硬盘**：硬盘可以被“挂载”，以便 Linux 能够以可启动的方式进行读写。更改将保存到硬盘。文件系统 CD 默认不挂载硬盘。只要卷具有读和写权限，操作系统就可以挂载硬盘。

![](img/72e1c6125676a623b5032cfdab8d797c_90_1.png)

- **可选闪存存储设备**：Linux 可以保存用户文件和设置，以保持重启重启之间的连续性。闪存盘通常用于此。![](img/72e1c6125676a623b5032cfdab8d797c_90_2.png)

- **RAM**：Live 文件系统发行版将文件写入临时硬盘。更改在会话（Session）期间保存。关闭 PC 电后，文件和设置将会。

图 4.5 Live Linux CD-ROM 工作原理图。除了作弊代码外，本书的附录 D 还包含一份快速上手指南，帮助你理解使用 Knoppix 的基础。该指南将涵盖如何启动 Knoppix 以及在操作系统中导航。在使用 CD-ROM 完成以下任何任务之前，阅读该指南可能会有所帮助：

### 试用

在购买每个新系统之前详细测试它，难道不是很好吗？这样可以解决在切换生产系统时的任何用户顾虑和不兼容性问题。在许多情况下，当企业无法确定一切都能正常工作时，有时你可以与旧系统并行启动一个系统，但很多时候这并不实际。现在考虑一下你的桌面上将会有什么样的操作系统。生产力的流失和其他故障可能会瘫痪运营。在不承诺更换操作系统的情况下测试和评估桌面的能力，对于那些评估迁移到 Linux 的人来说是一个极具吸引力的工具。

### 评估应用程序和文档兼容性

![](img/72e1c6125676a623b5032cfdab8d797c_91_0.png)

图 4.6 Knoppix 桌面与 Windows XP 非常相似，有一个开始按钮和可以从工具栏启动的应用程序。

### 测试 Linux 与 Office 的兼容性

测试 OpenOffice.org 套件作为 Microsoft Office 可能是你想要调查兼容性的第一个地方。如果你在本地存储办公文档，可以使用 OpenOffice.org 打开 Microsoft 文档，并确保它们是可读可编辑的。要实现这一点，只需查看 Knoppix 桌面上的硬盘导航到文档存储位置即可。如果你有一个分区，点击它将允许你打开硬盘并看到托管 Windows 安装的分区。一旦，你可以使用 Komfort 导航到“我的文档”文件夹。然后我们可以像图 4.7 所示启动 OpenOffice.org，查看文档在 OpenOffice.org 中是否可读。

![](img/72e1c6125676a623b5032cfdab8d797c_92_0.png)

图 4.7 OpenOffice.org 的 Writer 可打开在 Microsoft Office 中创建并存在硬盘上的 Word 文档。

### 实验室

可启动的 Linux 发行版解决了许多组织在训练方面的一个问题。如果你足够幸运拥有配备专用训练计算机的设施，那么这些计算机很可能运行某种版本的 Windows。建立 Linux 训练实验室可能非常耗时，但不必非如此。你可以刻制可启动 Linux CD-ROM 的副本，并将你当前的机器转换为临时的 Linux 工作站。此外，这不会让 PC 全天候承担 Linux 任务，因此你可以让 PC 产生多种用途。图 4.8 显示了一个使用 Knoppix CD-ROM 将每个 PC 转换为 Linux 客户端的实验室。你还可以以瘦客户端模式将 PC 连接到终端服务器，我们将在本章稍后部分进行演示。

### 使用 Live Linux CD-ROM Windows 训练实验室

![](img/72e1c6125676a623b5032cfdab8d797c_93_0.png)

| 类型 |  |
| :--- | :--- |
| Windows PC 训练实验室 | 现有训练实验室，带有运行 Windows 的 PC，用于 Linux 桌面迁移之前的业务正常操作。 |

![](img/72e1c6125676a623b5032cfdab8d797c_93_1.png)

| 转换后的 PC 训练实验室 | 现有训练实验室，带有从 Live Linux CD-ROM 运行 Linux 的 Windows PC。允许 PC 用于训练训练。 |

![](img/72e1c6125676a623b5032cfdab8d797c_93_2.png)

| 瘦客户端训练实验室 | 现有 PC 可以转换为如何使用新 Linux 桌面的临时瘦客户端。新的桌面环境搭建在服务器上，以便用户在完全沉浸新桌面环境之前尝试新软件和操作系统。服务器可以连接到转换后的工作站或带有瘦客户端软件的 Windows PC。 |

图 4.8 将 Windows 训练实验室转换为 Linux 训练实验室的选项。

### 76 Linux 业务桌面迁移

获得利益相关者的支持，正如我们之前提到的，对于迁移的成功至关重要。在迁移到 Linux 之前提供培训和试用可以让你至少有机会在训练实验室这样的非对抗性环境中推销解决方案的感知价值。此外，这也是开始听取用户反对意见并计划如何克服这些意见的好时机。

### Linux 的 IT 工具箱

Knoppix CD-ROM 带有生产力应用程序，还有一套强大的工具。当系统故障时，可以使用可启动的 Linux CD-ROM 从系统中救援数据。这个非常有价值的工具之所以有用，不仅是因为 CD-ROM 上的各种应用程序，还因为它的便携性。

#### 列表 4.1 标题大写格式的代码列表

```
knoppix@1[knoppix]$ lspci -v
0000:00.0 Host bridge: Intel Corp.
82845/GL[Brookdale-G]/GE/PE DRAM Control ler/Host-Hub Interface (rev
03)
```

```
Flags: bus master, fast devsel, latency 0
Memory at @0000000 (32-bit, prefetchable) [size=256M]
Capabilities: <available only to root>
```

```
0000:00:0.1 PCI bridge: Intel Corp.
82845/GL[Brookdale-G]/GE/PE Host-to-AGP B bridge (rev 03) (prog-if 00
[Normal decode])
```

```
Flags: bus master, 66MHz, fast devsel, latency 96
Bus: primary=00, secondary=01, subordinate=01,
sec-latency=32
```

```
I/o bridge: 00003000-00003fff
Memory bridge bridge: d0100000-d01fffff
Prefetchable memory bridge:
d8000000-ffffffff
```

```
0000:1d.0 USB Controller: Intel Corp. 82801DB/DBL/DBM
(ICH4-ICH4-M) U
SB UHCI Controller #1 (rev 02) (prog-if 00 [UHCI])
Subsystem: COMPAL Electronics Inc: Unknown device
```

```
Flags: bus master, medium devsel, latency 0, IRQ 16
I/O ports at 1800 [size=32]
```

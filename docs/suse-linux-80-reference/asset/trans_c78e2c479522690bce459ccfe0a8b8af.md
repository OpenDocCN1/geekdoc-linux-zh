

## 关于驱动程序和参数的一些提示

在介绍参数列表之前，这里有一些关于识别硬件、添加参数以及使用 SuSE 启动盘启动的提示：

- 大多数驱动程序都可以进行*自动探测*，例如测试此类硬件通常所在的各个标准地址。在自动探测期间，驱动程序可能会初始化一个不属于它的地址。这可能导致机器死机。
- 有些模块即使其硬件未安装也能成功加载。这主要适用于 3Com 网卡驱动程序。您应该先尝试自动探测。未使用的驱动程序可以轻松移除。然后，必须使用相应的参数启动未被自动识别的硬件。
- 最后，有些硬件组件有多个驱动程序（例如 NCR 53C810、Ultrastor）。据我们所知，两个 Ultrastor 驱动程序之间没有显著差异。NCR53C810 的 BSD 驱动程序还支持其他 NCR53C8xx 产品（例如 53C875），而旧的 NCR 驱动程序是唯一能识别 CD 刻录机的驱动程序。请选用适合您需求的那个。

### 参数

### 符号与含义

以下是按字母顺序排列的内核参数及相应设备列表。表 10.1 中的变量始终具有相同的含义。

| 变量 | 含义 |
|---|---|
| ⟨addr⟩ | 十六进制端口地址（如 0x300） |
| ⟨irq⟩ | 设备将使用的中断（如 7） |
| ⟨dma⟩ | 设备的 DMA 通道（如 1） |
| ⟨Start address⟩ |  |
| ⟨End address⟩ | 共享内存的十六进制内存分配 |

*表 10.1：内核参数中常用的变量*

我们主要关注成功安装所需的参数，但还有其他用于特殊用途的参数。大写字母很重要。

安装后，可以在 `/usr/share/doc/howto` 中的 `BootPrompt-HOWTO` 以及内核源代码文件 `/usr/src/linux/Documentation/kernel-parameters.txt` 中找到可能的内核参数的完整介绍。

### 启动提示符下的内核参数

本节列出的参数只能在启动提示符下传递给内核，例如在 SYSLINUX 提示符（包括启动盘）、LILO 提示符或使用 loadlin 时。

如果您打算将其中一个驱动程序作为模块安装，请参阅第 255 页*modprobe 参数*一节中的参数。

> **注意**
>
> 所有参数必须直接一个接一个地输入，用逗号分隔。参数之间不应有空格。

例如，要在启动提示符下输入 aha1542 的参数，请输入 `linux aha1542=0x300`。请记住，您始终必须在参数前面加上启动配置的名称。在 SuSE 启动盘上，这是名为 `linux` 的配置。

### 常规启动参数

某些参数可用于控制 Linux 内核的整体行为。

- *重启模式*（关闭 Linux）  
  `reboot={mode}`

  在这里，`{mode}` 有以下值：

  | 变量 | 值 / 含义 |
  |---|---|
  | `warm` | 热重启（不检查内存） |
  | `cold` | 冷重启（检查内存） |
  | `bios` | BIOS 重启 |
  | `hard` | CPU 崩溃重启（三重故障） |

  *示例：* `reboot=cold`

  这样会在关机后像按下了重置按钮一样启动机器。

- *保护内存段（reserve）*  
  `reserve={start1},{range1},...,{startN},{rangeN}`

  此参数允许您为那些对自动探测无响应（甚至可能因探测而崩溃）的硬件保留内存空间。

  示例：通过输入 `reserve=0x330,32 ether=5,0x330,eth0`，可以保护一块“敏感”的网卡不被自动探测和初始化。在此示例中，网卡具有 32 位数据总线，起始地址为 `0x330`，使用中断 5。

  有关网卡参数的完整说明，请参阅第 250 页*其他设备*一节。

- *放置根分区*  
  `root={partition}`

  | 变量 | 值 / 含义 |
  |---|---|
  | `{partition}` | 例如 `/dev/hda1`、`/dev/sdb5` |

  示例：`root=/dev/hda5`  
  这将启动内核，并尝试从扩展分区中的第一个逻辑驱动器将根分区加载到第一块（E）IDE 硬盘上。

- *RAM 大小（mem）*  
  `mem={size}`

  以字节、千字节（‘K’）或兆字节（‘M’）为单位输入 RAM 大小。对于 256 MB RAM，请输入 `mem=256M`。

  如果使用 Pentium 兼容品，请尝试 `mem=nopentium`。这可能会使其正常工作。

  这里随附的用于 i386 的标准内核以及较旧的 SMP 系统最多支持 4 GB。标准 SMP 内核配置为支持 64 GB。

- *使用 SMP 时的 CPU 数量*  
  `maxcpus={number}`

  使用 SMP 内核时，将 CPU 的最大数量设置为 `{number}`。

  示例：  
  `maxcpus=1`

- *串行控制台*  
  `console={device},{options}`

  设置系统控制台的设备。此参数可以多次使用。

  ```
  Examples:
  console=ttyS1,9600
  console=tty0
  ```

  更多示例请参阅 `/usr/src/linux/Documentation/serial-console.txt`。

### SCSI 控制器与 SCSI 子系统

大多数 SCSI 控制器都可以通过参数进行配置。

- *SCSI 流式磁带机*  
  `st={buffer},{threshold},{max}`

  | 变量 | 值 / 含义 |
  |---|---|
  | `{buffer}` | 缓冲区大小（1 KB 块的数量） |
  | `{write threshold}` | 写阈值（1 KB 块的数量） |
  | `{max}` | 最大缓冲区大小（可选）（例如 2） |

  示例：`st=1000,2000`

- *每个 ID 的 SCSI 设备数量*  
  `max_scsi_luns={number}`

  | 变量 | 值 / 含义 |
  |---|---|
  | `{number}` | `1..8` |

  示例：如果您只想使用第一个 LUN，则需要设置 `max_scsi_luns=1`。

  这通常用于 CD 换盘器，其中可用 CD 的数量等于参数 `max_scsi_luns=1` 的值。

- *Adaptec AHA-1520 / 1522 / 1510 / 1515 / 1505 SCSI 主机适配器*  
  `aha152x={ioaddr},{irq},{id},{rec},{par},{sync},{delay}[,{ext_tran}]`

  | 变量 | 值 / 含义 |
  |---|---|
  | ⟨id⟩（主机适配器的 SCSI ID） | 0, 1 |
  | ⟨rec⟩（重新连接） | 0, 1 |
  | ⟨par⟩（奇偶校验） | 0, 1 |
  | ⟨sync⟩（同步） | 0, 1 |
  | ⟨delay⟩ | 100 总线延迟，默认值 |
  | ⟨ext_trans⟩ | 0, 1 C/H/S 转换 |

  该驱动程序用于运行多个低成本 SCSI 控制器。所有带有 SCSI 控制器的声卡（Pro Audio Spectrum 除外）都可以通过安装的 Adaptec 芯片访问。

  对于所有非原装 152x，第四个参数（RECONNECT）似乎是必需的。对于大多数型号，必须将其设置为 ‘0’。只有 AHA2825 需要 ‘1’。

  *示例：* `aha152x=0x300,10,7`

- *Adaptec AHA-1540 / 1542 SCSI 主机适配器*  
  `aha1542={addr}[,{buson}[,{busoff}[,{DMA speed}]]]`

  | 变量 | 值 / 含义 |
  |---|---|
  | ⟨buson⟩ | 2..15 |
  | ⟨busoff⟩ | 1..64 |
  | ⟨DMA speed⟩ | 5、6、7、8、10 |

  *示例：* `aha1542=0x300`

- *Adaptec AHA-274x / 284x / 294x 主机适配器*  
  `aic7xxx={modifier}[,{modifier}[,...]]`

  | 变量 | 值 / 含义 |
  |---|---|
  | `{modifier}` | `extended`<br>激活硬盘几何结构的转换<br><br>`no_reset`<br>在主机适配器初始化时禁用 SCSI 总线重置<br><br>`irq_trigger:{x}`<br>仅适用于 EISA 系统<br>0 表示边沿触发，<br>1 表示电平触发<br><br>`verbose`<br>接收更多消息<br><br>`reverse_scan`<br>如果 BIOS 以错误的顺序处理多块卡<br><br>`7895_irq_hack:{x}`<br>-1 仅适用于 Tyan II 主板<br><br>`pci_parity:{x}`<br>如果完全不使用 pci_parity<br>奇偶校验为偶校验<br>0 不进行奇偶校验<br>1 奇校验<br><br>`tag_info:xxxx`<br>用于性能提升的队列管理，专家请参阅内核源代码 |

  **示例：** 如果机器在重置 SCSI 总线时挂起，则使用 `aic7xxx=no_reset`。仅在出现故障或功能异常时，才需要为基于 aic7xxx 的 SCSI 主机适配器设置参数。

  从 BIOS 1.3 版开始，AHA-2940 AU 不会再引起问题。可以从 Adaptec 支持部门获取更新。

  SCSI 主机适配器 Adaptec 2920 由 Future Domain 驱动程序驱动（请参阅第 246 页的 SCSI 控制器与 SCSI 子系统一节）。

- **Advansys SCSI 主机适配器**  
  `advansys={addr1},{addr2},...,{addrN}`

  **示例：** `advansys=0x110,0x210`

  此示例告诉内核在给定地址处搜索 Advansys 主机适配器。


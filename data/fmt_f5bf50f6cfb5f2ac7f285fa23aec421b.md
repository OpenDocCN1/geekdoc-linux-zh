
| TCP/IP主机名 | vmlinux6 | 由网络管理员分配；建议提前在DNS中设置，但不是必需的 |
| TCP/IP域名 | itso.ibm.com | 建议提前在DNS中设置 |
| TCP/IP网关 | 9.12.4.1 | 与本地子网通信的路由器 |
| DNS服务器1 | 9.12.6.7 | 由网络管理员分配 |
| DNS服务器2/3（可选） | — | 未使用 |
| OSA设备名称 | eth0 | 由IPWIZARD分配的接口名称 |
| OSA起始设备号 | 3020 | z/VM TCP/IP协议栈的OSA三元组起始编号 |
| TCP/IP地址 | 9.12.4.89 | z/VM系统的TCP/IP地址 |
| 子网掩码 | 255.255.252.0 | 由网络管理员分配 |
| OSA设备类型 | QDIO | 对于OSA/Express卡，通常为“QDIO” |
| 网络类型 | Ethernet | 通常为“Ethernet” |
| 端口名称（可选） | — | z/VM不需要 |
| 路由器类型 | None | 通常为“None” |
| VSWITCH的主OSA设备号 | 3024 | 指定第一个设备号（必须为偶数），接下来的两个设备号也将被使用 |
| VSWITCH的辅助OSA设备号 | 3028 | 应位于不同的CHPID/OSA卡上 |
| z/VM的DASD地址 | 1A20 - 1A24 | 用于承载z/VM的3390-3磁盘 |
| Linux的DASD地址 | 1A25 - 1A29 | 用于承载Linux客户机的3390-3磁盘 |
| 分页的DASD地址 | 8228 | 用于承载Linux交换空间的3390-3磁盘 |

在您使用附录B“规划工作表”（第403页）中提供的模板创建您的工作表，并规划好z/VM和Linux安装所需的全部资源后，我们就可以进行一些实际工作了。

> **注意：** 您应该熟悉z/VM的基本概念。如果不熟悉，请参阅第65页的2.8“z/VM基本命令入门”以及本章前面的各节。

## 4.3.2 从DVD安装z/VM

本节假设您已通过DVD将z/VM完成第一级安装到DASD上。请确保您：

- 完成附录B“规划工作表”（第403页）中的工作表。
- 能够访问硬件管理控制台（HMC），并使用具有进入单一对象操作模式权限的用户ID。

z/VM 5.3以磁带和DVD形式提供。由于磁带I/O速度更快，从磁带安装z/VM应该会更快，但是，从磁带安装可能需要更多次在HMC和磁带驱动器之间往返。

如果您熟悉HMC，可以使用两页的《z/VM自动安装与服务概要（DVD安装）》来替代或补充后面的说明。

如果您不熟悉HMC和z/VM，您可能需要查阅完整的安装手册《z/VM自动安装与服务指南 V5.3.0》，编号GC24-6099。在HMC中为系统设置LPAR超出了本书的范围；为z/VM创建LPAR与为z/OS创建LPAR没有区别。

如果您要在第二级安装z/VM（z/VM下的z/VM）或安装到SCSI磁盘，请使用z/VM手册，因为以下各节不介绍这些选项。

### 从DVD安装z/VM

本节说明如何从带有DVD-ROM的HMC将z/VM 5.3安装到等效于3390-3的DASD上。我们还会指出安装到更大的3390-9 DASD上的差异。对于其他配置，例如从磁带安装或安装到SCSI磁盘，请参阅z/VM文档。

要从DVD安装z/VM：

1. 在硬件管理控制台上，选择要安装z/VM的LPAR。
2. 如有必要，点击“跑道”按钮（右下角的两个环形箭头按钮）以导航到CPC恢复（有时仅命名为“恢复”）菜单。
3. 在CPC恢复菜单上，双击“集成3270控制台”，如图4-7（第146页）所示。将打开一个名为“<yourCPC>的集成3270控制台”的窗口（在较旧级别的HMC上，该窗口可能名为Personal Communications）。

> 提示：使用 `Alt+Tab` 键序列可在 HMC 窗口和 3270 控制台之间方便地切换。

![](img/b0a4b9056f819dccd4781a5105c92d45_161_0.png)

Figure 4-7 Integrated 3270 Console icon

4. 将“z/VM Product Package Version 5 Release 3.0” DVD 放入 HMC DVD 驱动器中。
5. 按如下方式进入单对象操作模式：

> 注意：在 z10 上，您无需进入支持元素（SE）模式即可从 DVD 加载。

a. 在 Views 区域中双击 Groups 图标。
b. 在 Groups Work Area 中双击 Defined CPCs。
c. 选择您的 CPC。
d. 如有必要，使用右下角带有圆形箭头的按钮导航到 CPC Recovery 菜单。
e. 双击 Single Object Operations 图标。点击 yes 确认。现在应出现一个新窗口，Primary Support Element Workplace，在旧版 HMC 上它将是“窗口中的窗口”。可能会出现一个关于证书的窗口。如果出现，请点击 OK。
f. 在此窗口顶部附近双击 Groups。
g. 在 Groups Work Area 中双击 Images。

> 重要：如果您无法进入单对象操作模式，您可能没有足够的权限。请咨询您的系统管理员。

6. 选择将安装 z/VM 的 LPAR。
7. 在此窗口中绕行到 CPC Recovery 菜单，如 Figure 4-8 所示。

![](img/b0a4b9056f819dccd4781a5105c92d45_162_0.png)

Figure 4-8 CPC Recovery menu

8. 双击 Load from CD-ROM, DVD, or Server 图标。“Load from CD-ROM or Server” 面板打开（Figure 4-9 on page 148）。

## Load from CD-ROM or Server - SCZP201:A04

Use this task to load operating system software or utility programs from a CD-ROM / DVD or a server that can be accessed using FTP.

Select the source of the software:

- Hardware Management Console CD-ROM / DVD
- FTP Source

Host computer:

User ID:

Password:

Account (optional):

File location (optional): `/cpdvd`

OK Cancel Help

Figure 4-9 Load from CD-ROM or Server panel

9. 选择 Hardware Management Console CD-ROM/DVD 按钮，如果它尚未被选中。
10. 在 File location 字段中输入 `/cpdvd`。这是 DVD 上包含 z/VM 5.3 安装代码的目录。
11. 点击 OK。
12. 加载 ramdisk。“Load from CD-ROM or Server” 面板中会显示软件列表。要加载 ramdisk：

a. 选择，如尚未选中，软件 `530vm.ins`，如 Figure 4-10 on page 149 所示，然后点击 OK。

![](img/b0a4b9056f819dccd4781a5105c92d45_164_0.png)

Figure 4-10 Selecting z/VM 5.3 ramdisk system

b. 在“Confirm the action”窗口中，点击 Yes。您应该会看到“Load from CD-ROM, DVD or Server Progress”窗口。DVD 驱动器上的绿色指示灯应亮起。
c. 当您看到消息 Completed successfully 时，点击 OK 关闭。这通常需要大约四到六分钟。

> 注意：尽管 z/VM ramdisk（`IBMVMMRAM`）大约在四到六分钟内加载，但已观察到较慢的加载时间（15-18 分钟）。当 DVD 驱动器上的绿色指示灯常亮时，加载时间是可以接受的。当它间歇性熄灭的时间多于亮起时，可能会导致加载时间过长。

您现在应该有一个在内存中运行的 z/VM 5.3 系统。本节中执行的任务类似于将 Linux 内核加载到内存中以进行安装。您可以将本节与第 4.4.2 节“Booting the Linux kernel for installation” on page 199 进行比较，并随后验证两个系统在安装开始前都将映像加载到主内存中。一个区别是 Linux 会自动启动安装程序，而在 z/VM 中您必须在下一节中所述调用命令。

## Copying a z/VM system image to DASD

要将 z/VM 复制到 DASD：

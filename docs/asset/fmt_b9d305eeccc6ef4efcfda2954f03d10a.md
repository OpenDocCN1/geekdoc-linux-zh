
Type `yum install gparted` (in Fedora) or `apt-get install gparted` (in Ubuntu) to install GParted. Run `gparted` as root to start it.

在调整 Windows 分区之前，你可能需要对其进行碎片整理。在某些 Windows 系统上，对磁盘进行碎片整理以使所有使用空间在磁盘上排序，请打开“我的电脑”，右键点击你的硬盘（通常是 C:），选择“属性”，点击“工具”，然后选择“立即碎片整理”。

磁盘碎片整理可能是一个相当长的过程。碎片整理的结果是磁盘上的所有数据都是连续的，从而在分区末尾创建大量连续的空闲空间。有时，你可能需要完成以下任务才能实现这一点：

- 如果在碎片整理期间没有移动 Windows 交换文件，你必须将其删除。在再次对磁盘进行碎片整理并调整大小后，你必须恢复交换文件。要删除交换文件，打开“控制面板”，打开“性能”选项卡，选择“虚拟内存”。要禁用交换文件，点击“无用虚拟内存”。
- 如果你的 DOS 分区中有位于你尝试释放的空间上的隐藏文件，你需要删除它们。在某些情况下，你无法删除它们。在在其他情况下（例如由程序创建的交换文件），你可以安全地删除这些文件。这很复杂，因为某些文件作为 DOS 系统文件不应被删除。你可以从根目录使用 `attr -s -h` 命令来处理隐藏文件。

磁盘完成碎片整理后，你可以使用前面描述的商业工具（Acronis Disk Director）重新格式化硬盘为 Linux 腾出空间。或者使用开源替代方案 GParted。

当你清理了足够的空间来安装 Linux（参见本章前面介绍的磁盘要求）后，你可以安装 Ubuntu、Fedora、RHEL 或其他 Linux 发行版。在安装期间设置引导加载程序时，你可以识别 Windows、Linux 以及任何其他可启动分区，以便在启动电脑时选择启动哪一个。

## 第三部分：成为 Linux 系统管理员

### 虚拟运行 Linux

使用虚拟化技术（如 `KVM`、`VMware`、`VirtualBox` 或 `Xen`），你可以配置你的计算机同时运行多个操作系统。通常，你运行着宿主机操作系统（如 Linux 或 Windows 桌面），然后配置在 във环境中运行的虚拟机操作系统。

如果你有 Windows 系统，可以使用商业性的 VMware 产品运行你的 Windows 桌面。访问 `http://www.vmware.com/try-vmware` 获取 VMware Workstation 的试用版。使用免费的 VMware Player 运行你已安装的虚拟机。使用完整版的 VMware Workstation，你可以同时运行多个发行版。

Linux 系统自带的可用虚拟化产品包括 VirtualBox (`http://www.virtualbox.org`)、`Xen` (`http://www.xen.org`) 和 `KVM` (`http://www.linux-xen.org`)。VirtualBox 最初由孙基系统公司开发。某些 Linux 发行版仍使用 Xen。然而，所有 Red Hat 系统目前都使用 KVM 作为 RHEL、Red Hat Enterprise Virtualization 以及其他云项目中 Red Hat 虚拟机功能的基础。关于在 KVM 宿主机上安装 Linux 作为虚拟机的信息，请参第 26 章。

### 使用安装选项

当 RHEL 或 Fedora 的内核启动时，内核命令行上提供的启动选项会修改安装过程的行为。通过在安装启动之前中断引导加载程序，你可以添加自己的启动选项来引导安装行为。

当你看到安装启动屏幕时，在引导加载程序运行时，按下 Tab 键或其他键即可编辑 anaconda 内核命令行。标识内核的行可能看起来如下所示：

```
mlinuz initrd=initrd.img ...
```

`vmlinuz` 是压缩后的内核，`initrd.img` 是 RAM 磁盘（包含启动安装程序所需的模块和其他工具）。要添加更多选项，只需在該行末尾输入它们并按回车。

因此，如果你在磁盘的 `/root/ks.cfg` 有一个可用的 kickstart 文件，你使用 kickstart 文件启动安装的 anaconda 引导过程可能如下：

```
mlinuz initrd=initrd.img ks=cdrom:/root/ks.cfg
```

对于 Red Hat Enterprise Linux 7 和最新的 Fedora 版本，安装期间使用的内核启动选项正在过渡到一种新方法。这种新命名前缀 `inst.` 可以放在本节中任何特定于安装过程的启动选项之前（例如，`inst.xdriver` 或 `inst.repo=dvd`）。

# 第 9 章：安装 Linux

然而，目前你仍然可以使用后面几节中带有 `inst.` 前缀的选项。

### 用于禁用功能的启动选项

有时，Linux 安装失败是因为计算机具有某些无法工作或不支持的硬件。通常，你可以通过向安装程序传递选项来解决这些问题。表 9.1 提供了一些示例：

#### 表 9.1 禁用功能的启动选项

| 启动选项 | 告诉系统 |
| :--- | :--- |
| `nofirewire` | 禁用火线接口 |
| `nodma` | 禁用 DMA |
| `noide` | 禁用 IDE |
| `nompath` | 禁用多路径 |
| `noparport` | 禁用并行端口 |
| `nopcmia` | 禁用 PCMCIA |
| `noprobe` | 不探测硬件 |
| `noscsi` | 禁用 SCSI |
| `nousb` | 禁用 USB |
| `ipv6` | 启用 IPv6 |
| `nonet` | 不探测网络 |
| `numa-off` | 禁用非统一内存内存访问 (NUMA) |
| `acpi=off` | 禁用高级配置和电源接口 (ACPI) |

如果你在视频方面遇到问题，可以按照表 9.2 所示指定视频设置。

#### 表 9.2 视频问题的启动选项

| 启动选项 | 告诉系统 |
| :--- | :--- |
| `xdriver=vesa` | 使用标准视频 |
| `resolution=1024x768` | 选择精确分辨率 |
| `nofb` | 不使用帧缓冲 |
| `skipdc` | 不使用 DDC |
| `graphical` | 强制图形安装 |

### 特殊安装类型的启动选项

默认情况下，在坐在控制台前以图形模式运行安装。如果你只有文本控制台，或者图形界面工作异常，你可以以文本模式运行安装：通过输入 `text` 使安装以文本模式运行。

如果你想在一台计算机上启动安装，但从另一台计算机上回答安装问题，你可以启用 `vnc`（虚拟网络计算）安装。启动这种类型的安装后，你可以到另一个系统并打开 `vnc viewer`，向其提供安装机器的地址（例如 192.168.0.99）。表 9.3 提供了必要的命令以及告诉系统做什么。

#### 表 9.3 VNC 安装的启动选项

| 启动选项 | 告诉系统 |
| :--- | :--- |
| `vnc` | 作为 VNC 服务器运行安装 |
| `vnconnect=hostname[:port]` | 连接到 VNC 客户端主机名和可选端口 |
| `vncpassword=<password>` | 使用密码（至少 8 位）连接到安装程序 |

### kickstart 和远程仓库的启动选项

你可以从包含内核和 RAM 磁盘之外的介质启动安装过程。如果是这样，你需要识别软件包所在的仓库。你可以通过提供 kickstart 文件来实现此点。要强制安装程序提示仓库位置（CD/DVD、硬盘、NFS 或 URL），请在安装启动选项中使用 `askmethod`。

使用 `repo=` 选项，你可以识别软件仓库的位置。以下示例显示了创建 `repo` 条目的语法：

```
repo=/dev/sda1:/myrepo
磁盘 1 分区上的 /myrepo 仓库

repo=http://abc.com/myrepo
Web 服务器上的 /myrepo 仓库

repo=ftp://example.com/myrepo
FTP 服务器上的 /myrepo 仓库

repo=cdrom
本地 CD 或 DVD 上的仓库

repo=nfs:mynfs.example.com:/myrepo/
NFS 共享上的 /myrepo 仓库

repo=nfsiso:nfs.example.com:/mydir/rhel7
来自 NFS 服务器的安装 ISO 镜像
```

你不需要直接识别存储库，而可以在 kickstart 文件中指定它。
以下是识别 kickstart 文件位置的一些方法。

```
ks=cdrom:/stuff/ks.cfg
从 CD/DVD 获取 kickstart。

ks=hda2:/test/ks.cfg

ks=http://www.example.com/ksfiles/ks.cfg
从 Web 服务器获取 kickstart。

ks=ftp://ftp.example.com/allks/ks.cfg
```

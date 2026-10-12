
方向键导航菜单。`<Enter>` 选择子菜单...（对于每个子菜单）
字母会被高亮。按下 `<Tab>` 选择某功能，而按下 `<Esc>` 排除某功能。按下
图例：`[*]` 功能已选中，`[ ]` 功能被排除

![](img/bc86631e65e541c1c58ec0ab72a978e0_375_4.png)

# 第 13 章：嵌入式 Linux 简介

## Busybox

![](img/bc86631e65e541c1c58ec0ab72a978e0_376_0.png)

![](img/bc86631e65e541c1c58ec0ab72a978e0_376_1.png)

# 第 13 章 嵌入式 Linux 简介

![](img/bc86631e65e541c1c58ec0ab72a978e0_377_0.png)

方向键导航菜单；`Enter` 选择子菜单，`--` 用于空子菜单。高亮的字母为加粗。按下 `<` 选择某功能，按下 `>` 排除某功能。按下 `<Esc>` 退出，`<F>` 帮助，`/` 搜索。图例：`*]` 功能已选中，`[ ]` 功能被排除

```bash
footroot-stm32
ubub needs a toolchain in w/char ***
make-root
smd-bootloader
smd-mraboot
```

- 选择主机需要的选项。

![](img/bc86631e65e541c1c58ec0ab72a978e0_377_1.png)

- 保存配置并运行 `make` 命令开始构建过程。

![](img/bc86631e65e541c1c58ec0ab72a978e0_377_2.png)

# 第 13 章 嵌入式 Linux 简介

- 等待构建完成。`rootfs` 将生成在 `output/images` 目录下。

- 将 `rootfs` 拷贝到你的 `CortexA9` 平台，并使用你的引导程序启动它。

> 将 `RootFS` 拷贝到第二个分区

```
embedded-system-embedded-KS:/media/embedded-system-ks/embedded-system-ks/LABS/Linux/LABS/mount cd /sd1
embedded-system-kembedded-KS:/media/embedded-system-ks/embedded-system-ks/LABS/Linux/LABS/mount p2 sudo
rm -rf /bin /dev /etc /lib /linux /mnt/proc /root rootfs.tar.gz zbin/sys/tmp/var/
```

```
embedded-system-embedded-KS:/media/embedded-system-ks/embedded-system-ks/LABS/Linux/LABS/mount p2 cp ../../build
rootfs-30180930/images/rootfs/ p2
```

![](img/bc86631e65e541c1c58ec0ab72a978e0_378_0.png)

不要忘记在 `/dev/ttyAM0` 下创建一个文件

`sudo mknod /rootfs/dev/ttyAM0 c 4 64`

![](img/bc86631e6554c58ec0ab72a978e0_378_1.png)

# 启动 LINUX

![](img/bc86631e65e541c1c58ec0ab72a978e0_378_2.png)

# 进入登录界面

# 第 15 章：嵌入式 Linux 简介

![](img/bc86631e65e541c1c58ec0ab72a978e0_379_0.png)

# 内核配置（附录）

这里是针对不同场景的内核配置示例：

1. 嵌入式系统：对于具有特定硬件的嵌入式系统，你可能希望内核包含特定的功能：
   - 处理器类型：选择嵌入式系统的架构。
   - 设备驱动：启用必需的设备驱动，如 `devtmpfs`。
   - 文件系统：启用必需的文件系统，如 `ext4`。
   - 网络支持：启用网络支持，如 `TCP/IP`。
   - 电源管理：启用电源管理。
2. 桌面系统：对于具有高性能的桌面系统，你可能希望内核包含更多功能。示例包括：
   - 处理器类型：选择桌面系统的架构。
   - 设备驱动：启用各种设备驱动，如蓝牙、`WiFi`。
   - 文件系统：启用文件系统，如 `NTFS`。
   - 网络支持：启用网络支持，如 `VPN`。
   - 电源管理：启用电源管理。
3. 高可用性系统：对于具有高可用性的系统，你可能希望内核包含特性。示例包括：
   - 处理器类型：选择高可用性系统的架构。
   - 设备驱动：启用存储设备驱动，如 `RAID`、`iSCSI`。
   - 文件系统：启用文件系统，如 `NFS`、`SMB`。
   - 网络支持：启用网络支持，如 `VLAN`。
   - 电源管理：启用电源管理。

内核配置取决于具体需求。以下是适用于所有架构的一些菜单：

- 代码选项
- 通用设置 (`General setup`)
- 可加载模块支持
- 网络
- 块设备
- 设备驱动
- 文件系统
- 内核黑客 (`Kernel hacking`)
- 安全选项

# 第 13 章 嵌入式 Linux 简介

## 通用设置

此部分包含你应该开启的三个设置：

- 匿名内存分页支持交换分区
- `System V` 启用进程间通信
- `Sysctl` 允许通过 `/proc` 更改内核参数

![](img/bc86631e65e541c1c58ec0ab72a978e0_381_0.png)

- 本地版本 - 附加到内核
  变量名：`LOCALVERSION`
  在内核版本末尾附加一个额外的字符串。这会在显示名称时显示。

- 可选自动附加版本信息
  变量名：`LOCALVERSION_AUTO`
  通过查找指向顶部的 `git` 标签自动确定当前树是否为发布树。

![](img/bc86631e65e541c1c58ec0ab72a978e0_381_1.png)

- 匿名内存分页支持（交换）
  变量名：`SWAP`
  依赖 `MMU`
  这允许你选择是否支持交换设备或交换文件，用于提供比计算机实际内存内存的虚拟内存。

![](img/bc86631e65e541c1c58ec0ab72a978e0_381_2.png)

- `System V IPC`
  变量名：`SYSIPC`
  依赖 `MMU`
  进程间通信是一组库函数和系统调用，允许异步运行的进程共享信息。它通常被认为是一件好事，因此程序可以在不需要你说的情况下运行：

| `System V IPC` |
| :--- |
| 消息队列 |
| 共享内存 |
| 信号量 |

## 第 13 章：嵌入式 Linux 概览

- 选项：`POSIX` 消息队列
- 变量名：`POSIX_MQUEUE`
- 依赖于 `NET` & `EXPERIMENTAL`
- `POSIX` 消息消息队列是 `IPC` 的一部分。每条消息都有一个优先级，决定了进程接收消息的顺序。如果你想针对例如 `Solaris` 编写的代码使用 `POSIX` 消息队列（函数 `mq_*`）进行编译和编程，请在此处选择 `Y`。

![](img/bc86631e65e541c1c58ec0ab72a978e0_382_0.png)

- 选项：`BSD` 进程会计
- 变量名：`BSD_PROCESS_ACT`
- 如果你想让用户程序能够指示内核（通过特殊的系统调用）将进程信息写入文件：每当进程退出时，内核都会将该进程的信息附加到文件中。

- 选项：`BSD` 进程会计版本 3 格式
- 变量名：`BSD_PROCESS_ACT_v3`
- 如果在此处选择 `Y`，进程会计信息将以新格式写入，该格式还会记录每个进程的进程 ID。

![](img/bc86631e65e541c1c58ec0ab72a978e0_382_1.png)

- 选项：内核配置支持
- 变量名：`IOCONFIG`
- 此选项允许将 `Linux` 内核的配置文件存储在内核中。它提供了运行中的内核或磁盘上内核使用了哪些内核选项的文档。这些信息可以通过 `extract-config` 脚本从内核镜像文件中提取，用于重新构建内核或构建另一个内核。如果启用（默认开启），也可以通过 `/proc/config.gz` 从运行的内核中提取。

![](img/bc86631e65e541c1c58ec0ab72a978e0_382_2.png)

- 选项：`Cuset` 支持
- 变量名：`CPUSETS`
- 此选项允许你通过创建和管理 `CPUSets` 动态将系统划分为 `CPU` 组，并将进程分配给这些组。这对于大型 `SMP` 或多核系统特别有用。

例如，以下命令序列将设置一个名为 `"Charlie"` 的 `cuset`（仅包含 `CPU 0` 和 `1` 以及内存节点），然后启动进程：

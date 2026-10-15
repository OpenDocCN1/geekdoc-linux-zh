

| 目标 | 摘要 |
|---|---|
| 2. 使用命令行工具配置 LVM | 要初始化一个用于 LVM 的分区，请使用工具 **pvcreate**。 |
|  | **pvscan** 显示物理卷及其使用情况。 |
|  | 工具 **pvmove** 用于将数据从一个物理卷移动到另一个物理卷。 |
|  | 工具 **vgcreate** 用于创建新的卷组。 |
|  | 要向组中添加更多物理卷，请使用 **vgexpand**。 |
|  | 删除未使用的物理卷是在使用 pvmove 将计划删除的物理卷上的数据转移到其他物理卷之后，使用 **vgreduce** 完成的。 |
|  | **vgremove** 删除卷组，前提是该组中没有逻辑卷。 |
|  | 要创建逻辑卷，请使用 **lvcreate**。 |
|  | **lvscan** 用于查看逻辑卷。 |
|  | **lvextend** 用于增加逻辑卷的大小。 |
|  | 在使用 **lvreduce** 减小逻辑卷大小之前，您必须先减小文件系统的大小。 |

## 第 5 节 使用 NetworkManager 配置网络

如果您在笔记本电脑上使用 SUSE Linux Enterprise Server 10，您很可能会根据所在位置使用不同类型的 Internet 访问——也许是在办公室的局域网，在客户现场的无线连接。

### 目标

- 1. 使用 NetworkManager 配置网络

### 目标 1

## 使用 NetworkManager 配置网络

传统的网络设置要求您切换到 root 账户才能更改网络配置。NetworkManager（软件包 NetworkManager）的目的是允许用户根据需要更改网络配置，而无需切换到 root 账户。

NetworkManager 以 root 用户系统级守护进程的形式运行，因为直接操作硬件需要 root 权限。用于此目的的程序是 /usr/sbin/NetworkManager 和 /usr/sbin/NetworkManagerDispatcher。nm-tools 可用于列出有关 NetworkManager、设备和无线网络的信息。

从系统中当前安装的所有适配器列表中，NetworkManager 首先尝试有线适配器，然后尝试无线适配器。支持无线扫描的无线适配器优先于不支持的适配器。NetworkManager 不会尝试尽可能长时间保持连接，这意味着插入有线网络会将连接切换到有线网络，远离无线网络。

对于无线网络支持，NetworkManager 保留两份无线网络列表：受信任列表和首选列表。受信任列表包含用户明确添加到其中的网络，而首选列表包含用户强制 NetworkManager 连接的网络。

由于受信任和首选网络是特定于用户的，因此必须有某种机制来获取和按用户存储此信息。这是通过桌面级按用户进程 nm-applet 或 KDE 中的 KNetworkManager 实现的。NetworkManager 通过 DBUS 与这些用户级进程通信。

在 YaST 中选择 NetworkManager 也会自动在用户登录时启动网络小程序。使用桌面小程序，用户可以轻松更改网络配置：

# 图 5-2

![](img/8279afe915b153902294b0e58311b75a_89_0.png)

注意：拍摄上述屏幕截图的计算机上没有内置无线网卡，因此该屏幕截图中没有切换网络的选项。

## 使用 NetworkManager 配置网络

| 目标 | 摘要 |
|----------|---|
| 1. 使用 NetworkManager 配置网络 | NetworkManager 允许用户更改网络配置而无需承担 root 权限。 |
|  | NetworkManager 主要适用于笔记本电脑使用。 |

## 第 6 节 管理用户访问和安全

在本节中，您将学习如何执行基本的用户和组管理任务，为用户提供安全且可访问的 SUSE Linux Enterprise Server 环境。

### 目标

- 1. 使用 PAM 配置用户身份验证
- 2. 配置安全设置


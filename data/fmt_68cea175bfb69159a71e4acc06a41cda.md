
如果你以 `root` 用户身份输入 `linuxconf<ENTER>` 命令，将不会提示你输入 `root` 密码。相反，将显示图 3.2 所示的 `Linuxconf` 窗口。打开 `Linuxconf` 窗口后，使用以下步骤进行文件系统挂载：

1. 如果主窗口没有显示 `Config` 页面，点击 `Config` 标签卡显示它。
2. 如果主菜单中的 `File systems` 子部分未展开，点击 `File systems` 旁边的加号将其展开。
3. 点击 `File systems` 子菜单中的 `Access local drive` 条目。`Linuxconf` 将显示如图 3.3 所示的 `Access local drive` 页面。该页面列出了所有当前挂载的文件系统。

![](img/1a9080c03c91a8cc232a677fdc119548_143_0.png)

图 3.3 `Linuxconf` 的 `Access local drive` 页面。

4. 点击 `Access local drive` 页面上的 `Quit` 按钮。`Linuxconf` 将关闭 `Access local drive` 页面。

### 提示 3.1.4：使用 Linuxconf 创建本地挂载

使用 `Linuxconf`，你可以定义文件系统挂载。要做到这一点，首先从终端窗口输入命令 `linuxconf<ENTER>` 来启动 `Linuxconf`。你必须是 `root` 用户才能使用 `Linuxconf`。在认证对话框中提供 `root` 密码并按回车。`Linuxconf` 将启动并显示如图 3.2 所示的初始界面。打开 `Linuxconf` 窗口后，使用以下步骤定义文件系统挂载：

1. 如果主窗口没有显示 `Config` 页面，点击 `Config` 标签卡显示它。
2. 如果主菜单中的 `File systems` 子部分未展开，点击 `File systems` 旁边的加号将其展开。
3. 点击 `File systems` 子菜单中的 `Access local drive` 条目。`Linuxconf` 将显示图 3.3 所示的 `Access local drive` 页面。该页面列出了在 `/etc/fstab` 中挂载的所有文件系统，并指示哪些正在挂载。
4. 点击 `Access local drive` 页面上的 `Add` 按钮。`Linuxconf` 将显示如图 3.4 所示的 `Volume specification` 页面。

![](img/1a9080c03c91a8cc232a677fdc119548_144_0.png)

图 3.4 `Linuxconf` 的 `Volume specification` 页面。

5. 在 `Volume specification` 页面 `Partition` 字段中输入要挂载的分区。例如，为 `/dev/hda6` 定义挂载点路径 `/homedir`，在 `Partition` 字段中输入 `/dev/hda6`。
6. 点击 `Volume specification` 页面 `Type` 字段右侧的箭头，选择第 5 步中指定分区的文件系统类型。`Linux` 分区为 `ext2` 类型，`DOS` 分区为 `msdos` 类型，`Windows` 95 和 98 分区为 `vfat` 类型。

## 让 Linux 运行起来：核心技巧与技术

7. 进入卷规格页的挂载点文本框。例如，要为 `/dev/hda6` 的挂载点定义为路径 `/path/somedir`，请在 `Mount point`（挂载点）文本框中输入。
8. 点击鼠标卷规格页上的 `Options`（选项）选项卡。`Linuxconf` 随后会显示卷规格页的 `Options` 选项卡，如图 3.5 所示。

![](img/1a9080c03c91a8cc232a677fdc119548_145_0.png)

9. 如果你想让分区以只读模式挂载，请确保选中了 `Read`（只读）复选框。如果没有，请点击复选框进行选中。
10. 如果你不想让分区在启动时自动挂载，请确保选中了 `Not mount at boot time`（启动时不挂载）复选框。如果没有，请点击复选框进行选中。
11. 点击 `Linuxconf` 窗口中卷规格页上的 `Accept`（接受）按钮。`Linuxconf` 随后会将分区定义添加到 `/etc/fstab` 文件中，关闭卷规格页并显示 `Access local drive`（访问本地驱动器）页。
12. 点击 `Linuxconf` 窗口中 `Access local drive` 页上的 `Quit`（退出）按钮。`Linuxconf` 随后会关闭 `Access local drive` 页。

## 技巧 3.1.5：判断你是否需要交换分区（Swap Partition）

每一个高级的多任务处理操作系统（包括 `Linux` 和 `Windows` `NT`）都使用虚拟内存。虚拟内存是一种技术，物理内存（`RAM`）有限的计算机通过使用部分可用磁盘空间来模拟 `RAM`，使其看起来拥有比物理可用内存更多的内存。

# 第 3 章：管理文件、目录和磁盘

在 `Windows` `NT` 中，这是通过创建一个或多个隐藏的交换文件（swap files）来实现的，现有硬盘分区使用这些文件来存储数据。该文件被称为交换文件，因为操作系统在处理需要数据时，会在物理内存和交换文件之间交换数据。

在运行 `Linux` 时，你可以使用交换文件或交换分区来创建虚拟内存。`Linux` 中的交换文件与 `Windows` `NT` 中使用的文件一样，是在 `Linux` Native（原生 `Linux`）分区上创建的特殊文件，也可以用于存储其他文件。相比之下，交换分区是一个专门为虚拟内存任务而经过特殊格式化的磁盘分区。

在 `Linux` 中，强烈建议创建一个专用的交换分区。该分区可以是硬盘上带有几个其他分区的其中一个，或者对于高负载使用的系统，可以是硬盘上专门用于交换任务的唯一分区。基本规则是：一个带有单一交换分区的专用硬盘提供的性能优于在许多分区中包含一个交换分区的硬盘，而后者的性能又优于交换文件。

对于大多数桌面用户和低端服务器，共享硬盘上的交换分区已经绰绰有余了。

关于 `Linux` 交换分区的需要记住的一些通用原则：

- `RedHat` `Linux` 要求内存为 `16MB` 或更小的系统应有一个交换分区。
- 交换分区的最大大小可达 `127MB`。
- 系统可以拥有多个交换分区。
- 通常情况下，你需要总等于系统总物理内存的交换空间。
- 如果你正在运行文件密集型应用程序（例如高频使用的 `Web` 服务器），你可能需要比系统物理内存更多的交换空间。

## 3.1.6：fdisk 接口概览

`fdisk` 程序是目前 `Linux` 中配置磁盘分区最常用的工具，对所有 `Linux` 高级用户来说都是非常熟悉的。因此，`RedHat` 在 `RedHat` `Linux` 6.1 版本中提供了 `fdisk` 作为 `Disk` `Druid` 的替代工具，用于配置磁盘分区。

使用 `fdisk` 时，你单独处理每个物理磁盘，而不是像使用 `Disk` `Druid` 那样一次处理所有磁盘。要编辑磁盘分区，使用以下命令：

```
$ fdisk /dev/hda
```

# 让 Linux 运行起来

确保将 `/dev/hda` 替换为你要操作的设备文件。`fdisk` 将显示如图 3.6 所示的初始 `fdisk` 界面。

```
磁盘磁道数设置为 242。
没问题，但它比 1024 大。
分区可能需要很长时间（例如旧版本的 fdisk v1.0）。
分区可能受到其他操作系统的影响（例如 DOS, GPT）。
Command (m for help): ?
```

图 3.6 初始 `fdisk` 界面

`fdisk` 通过输入单字符命令并按回键来操作。某些命令需要额外信息，`fdisk` 会提示你。两个实用的 `fdisk` 命令是 `m` 或 `?`。这些命令会显示一个如图 3.7 所示的帮助界面。该帮助界面列出了所有常用的 `fdisk` 命令及其描述。

```
Command (m for help): ?
设置可启动标记
切换 dos 属性
或标签类型
列出分区类型
打印主分区表
创建新分区表
打印现有分区表
退出不删除
创建新文件系统
更改设备单位
更改签名
write
```

图 3.7 帮助界面。

```
Command (m for help): ?
设置可启动标记
切换 dos 属性
或标签类型
列出分区类型
打印主分区表
创建新分区表
打印现有分区表
退出不删除
创建新文件系统
更改设备单位
更改签名
write
```

```
Command (m for help）：
设置可启动标记
切换 dos 属性
或标签类型
列出分区类型
打印主分区表
创建新分区表
打印现有分区表
退出不删除
创建新文件系统
更改设备单位
更改签名

```

```
Command (m for help): ?
设置可启动标记
切换 dos 属性
或标签类型
列出分区类型
打印主分区表
创建新分区表
打印现有分区表
退出不删除
创建新文件系统
更改设备单位
更改签名
write
```

```
Command (m for help): ?
设置可启动标记
切换 dos 属性
或标签类型
列出分区类型
打印主分区表
创建新分区表
打印现有分区表
退出不删除
创建新文件系统
更改设备单位
更改签名
write
```

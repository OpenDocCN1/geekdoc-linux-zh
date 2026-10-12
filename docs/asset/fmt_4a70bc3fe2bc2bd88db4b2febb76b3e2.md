
### 列表 23.2 Lilo.conf 文件设置为两个 Linux 内核之一，以及一个 DOS 分区

```
boot=/dev/sda hda2
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
image=/boot/vmlinux-2.2.12
label=linux
append="ether=0,0,eth ether=0,0,eth1"
root=/dev/sda1 hda2
read-only
image=/boot/vmlinux-2.2.7-1.15 .old
label=old d
root=/dev/sda1 hda2
read-only
other=/dev/sdb hda1
label=dos
table=/dev/sdb hda
```

# 启动到特定的运行级别

你可以通过在 LILO 提示符向内核传递命令行参数来覆盖 Linux 启动的运行级别。例如，要进入单用户模式，在 LILO 提示符处输入以下命令（你可以用 `i` 替换单词 `single`）：

```
lilo: linux single
```

单用户模式是 UNIX 系统的维护模式，不会启动任何守护进程、网络或登录程序。这从根本上确保了系统成功启动（只要硬盘、内核文件等是正常的）。要启动另一个运行级别（例如，测试其配置是否正确），将运行级别数字设置为 LILO 提示符处内核命令行的最后一项。

你可以对 `lilo.conf` 文件中的 `append` 命令进行此类更改，但我建议你不要这样做。相反，请按照第 26 章“管理网络连接”中的描述修改你的 `inittab` 文件。

有些事情是你真的不想在 LILO 命令提示符下做的。例如，不要将系统设置为级别 0 或 6（分别是关机和重启），因为系统会很乐地启动——但随后会立即关机。

# 使用 LOADLIN

`LOADLIN` 设计用于从 DOS 提示符启动 Linux，这意味着可能从 DOS 启动 Linux 而无需实际重启机器。这具有固有的优势，因为除了创建 Linux 数据和交换分区外，它的工作不需要对硬盘结构进行任何修改。

存在另一个优势与不支持的硬件有关。特别是声卡，通常具有 SoundBlaster 仿真模式，这些模式只能通过使用 DOS 程序来访问。因为 `LOADLIN` 不重启机器，声卡将保持在与 SoundBlaster 兼容的模式，允许 Linux 驱动程序与其工作。我不建议这样做，但这是一个选项。对我来说，`LOADLIN` 非常方便。

# 从 DOS 启动 Linux

设置 `LOADLIN` 比 LILO 简单，因为 `LOADLIN` 作为普通的 DOS 程序运行，并获取从 Linux 启动所需的所有信息。例如，以下命令使 LOADLIN 加载内核镜像 `vmlinuz` 并指向分区 `/dev/hda4`，只读：

```
loadlin vmlinuz /dev/hda4 ro
```

# 设置 LOADLIN

`LOADLIN` 归档在主 Linux 软件发行点 http://metalab.edu/。如果你是通过光盘购买的 Linux，值得先查看那些磁盘，因为 Linux 归档通常非常繁忙。截至本文 `LOADLIN` 的发行版本为 1.6，文件为 `loadlin16.tgz`。最新版本可以在 Sunsite（通过 FTP 访问）的 `/pub/system/dualboot/` 目录下找到。当你拥有文件后，可以通过以下命令将其提取到自己的目录：

```
tar xzf lodlin16.tgz
```

`LOADLIN` 带有一个用于启动 Linux 的示例批文件。该文件必须根据你的特定设置进行修改。

# 设置 LOADLIN 和批文件

1. 你需要知道安装 Linux 的分区。要这样做，输入以下内容：

```
$ mount 结果如下：
/dev/hda4 on type ext2 (rw)
/proc on /proc type proc (rw)
/dev/hdb7 on /mnt/f type vfat (rw)
/dev/sda on /mnt/zip type vfat (rw,nosuid,nodev)
```

这向你展示了 Linux 挂载的分区以及分区的位置。根分区（即挂载在 `/` 挂载点的分区）是 Linux 启动的分区。在这种情况下，`/dev/hda4` 就是你的根分区。你可能在安装系统时已经注意到此信息，如果是这样，你可以跳过此步骤。

- 2. 你需要了解系统所需的任何内核参数（例如，你是否有两个网络适配器）。检查内核参数的最好方法是检查当前安装目录中 `l110.conf` 文件中的 `append` 命令。大多数系统对任何关键部分都不需要参数，多网卡切换除外。

- 3. 你需要知道内核文件本身的名称，它通常是 `/boot/vmlinuz`。遗憾的是，这在不同的发行版之间有所不同。

> 为什么内核被称为 vmlinuz？

结尾的 `z` 是因为内核镜像使用了类似于 gzip 的方法进行压缩，以减少占用的磁盘空间；镜像在启动时会被解压缩。如果你真的想这样做，可以更改内核文件的名称；但请确保你将 LILO 指向正确的文件！

- 4. 确定你的机器启动是否需要初始内存磁盘（`initrd`）。初始内存磁盘由引导加载程序加载，包含了 Linux 访问启动所需的实际设备所需的设备驱动程序。例如，大多数 SCSI 适配器允许在没有设备驱动的情况下进行简单的 DOS 访问，但 32 位操作系统无法使用这种方法。引导加载程序（如 LILO 和 `LOADLIN`）使用 DOS 方法加载内存磁盘和内核，然后内核从内存磁盘加载设备驱动模块以继续启动系统。

如果你有 SCSI 适配器，你通常需要使用 `initrd`。

- 5. 获取内存磁盘文件 `/boot/initrd-2.0.31.img`。确保该文件的版本号与你正在使用的内核版本一致！

## 设置 LOADLIN 启动盘

- 1. 使用 DOS 或 Windows 95 格式化一张可启动的软盘。在 DOS 或 Windows 95 命令行提示符，输入以下内容：

```
format a: u /s
```

`u` 参数防止 DOS 6.x 将未格式化信息保存到磁盘，还能加快操作速度。理论上，DOS 放在磁盘上的未格式化信息可以让你在不小心格式化磁盘后从磁盘恢复数据。然而，在向磁盘写入大量数据后，是不可能取消格式化的。

- 2. 将文件 `loadlin.exe`（程序本身）、`vmlin`（Linux 内核）和 `initrd-2.0.31.img`（初始内存磁盘，如果需要的话）拷贝到软盘。你需要将 `initrd-2.0.31.img` 重命名为 `initrd.img` 以获得 DOS 支持的短文件名。

- 3. 使用你喜欢的文本编辑器在软盘上创建一个 DOS 批处理文件。你可以将文件命名为 `autoexec.bat`。否则，将其命名为 `linux.bat`。此文件将使用正确的参数列表调用 `LOADLIN`。你可以每次手动执行，但使用批处理文件可能更方便。你可能想在软盘的 `autoexec.bat` 和 `config.sys` 文件中添加 DOS 音频驱动、启动菜单或其他对象（现在或以后）。但是，不要添加 `EMM386.EXE` 驱动程序，因为该驱动程序会导致你在使用 `LOADLIN` 启动 Linux 时遇到很多麻烦。

告诉 `LOADLIN` 在不使用初始内存磁盘的情况下启动系统的命令如下：

```
loadlin vmlinuz root=/dev/hda2 ro
```

如果你必须使用初始内存磁盘，请使用以下：

```
loadlin vmlinuz initrd.img root=/dev/hda2 ro
```

此示例假设你的系统从分区 `/dev/hda2` 启动。结尾的 `ro` 告诉 Linux 内核最初将根文件系统挂载为只读。这允许你在需要时检查文件系统。

- 4. 尝试一下。记住，如果你没有将 `loadlin` 命令放在磁盘上，你必须颁发 `linux` 命令来运行 `linux.bat` 批处理文件。

## 使用 LOADLIN 传递内核参数

`LOADLIN` 将第一个参数（它期望为内核名称）之后的所有内容解释为内核参数。因此，要使用 `LOADLIN` 启动 Linux 到级别 5，请使用以下命令：

```
loadlin vmlinuz root=/dev/hda2 ro 5
```

上一个命令假设你的 Linux 根分区是 `/dev/hda2`。如果你从软盘启动，且 `LOADLIN` 看到某些 `LOADLIN` 头部版权信息或关于你当前操作系统（如 DOS）的一些信息，`LOADLIN` 将开始加载内存磁盘和内核镜像，并在过程中显示点。系统随后会启动内核。如果你从硬盘运行 `LOADLIN`，那么这一切发生得快到看不见——除非你有一台旧机器。

# 第 24 章

## 管理用户和组

- 用户、组及其与系统的关系
- 使用 `usercfg` 工具
- 使用命令行添加、编辑和删除用户
- 添加、编辑和删除组
- 修改用户和组所有权
- 修改文件所有权和权限
- 高级概念：密码认证模块

第五部分 系统管理

第 24 章 管理用户和组

### 用户、组及其与系统的关系

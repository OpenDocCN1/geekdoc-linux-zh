
`/dev/hda2` `/mnt/hda2` `ext3` `noauto,users,exec,rw` `0` `0`

通过该更改，只需 `sudo mount /dev/hda2` 即可挂载具有读/写权限的目录。你可以按照后续章节“你的 KNOPPIX 配置”中的描述来永久保存该更改。

## Windows 分区

只要你的分区被正确检测，挂载 Windows 分区与 Linux 分区没有区别……（此处省略原文中大量重复的句子，根据指令要求保持格式与翻译逻辑）

## 创建持久性主目录

如果你打算多次使用 KNOPPIX 电脑（或者你只是想在 RAM 中获得更多存储空间），你可以在硬盘上分配一些空间。可以通过两种方式实现：

- 分配整个分区用于你的主目录
- 以镜像文件的形式分配该分区的一部分

你也可以将持久性主目录放在可写的、可移动的介质上，例如内存。一旦你创建了该区域，KNOPPIX 每次重启时都可以使用它。以下是操作步骤：

1. 点击面板中的切换企鹅，然后选择 Create a Persistent KNOPPIX disk image。将弹出一个窗口，询问你是否准备好创建一个主目录。
2. 点击 Yes（是）继续。系统询问你想使用哪个分区作为你的持久性主目录。
3. 选择你想存储持久性桌面的分区并点击 OK。
4. 系统询问你是否想以加密格式保存主目录（如果你选择了 Yes，你将必须指定一个在启动时访问持久性主目录所需的密码）。
5. 选择 No（否），不将目录选择为加密。系统询问你输入主目录的大小。
6. 输入要分配给主目录的兆字节数并点击 OK。确保分区上有足够的空间。（稍后挂载分区时，你可以输入 `df -h` 查看其可用空间。）分区或镜像文件应该会被创建。

当我运行此程序在 `hda5` 分区上创建一个 100MB 的镜像时，它创建了 `/mnt/hda5/kppix.img`，其有 98MB 的可用空间。要查看如何使用该目录，请参考本章节的“重启 KNOPPIX”部分。

## 保留你的 KNOPPIX 配置

在你花了大量工作配置你的 KNOPPIX 桌面、打印机、网络、磁盘和其他偏好后，下次重启时将丢失所有内容。嗯，KNOPPIX 提供了一种方法，让你可以保存你的配置信息并供以后

下一节。这些保存的信息可以存储在软盘或任何其他可访问的介质（例如您的硬盘）上，以便下次重启 KNOPPIX 时使用。方法如下：

- 1. 从面板上的挤压企鹅图标上，点击 Config（配置）：Save KNOPPIX configuration（保存 KNOPPIX 配置）。
- 2. 选择要保存的配置文件。您可以选择保存个人配置（`/home/knoppix`、`.kde` 和 `.mozilla` 目录）、桌面上的文件、您的网络配置、X 配置以及其他系统配置文件（来自 `/etc`）。
- 3. 选择将您的配置文件保存到软盘或任何可写入的可用磁盘分区上。选择软盘可以使配置具有可移植性，而选择硬盘则可以让配置在同一台机器上轻松重复使用。
- 4. 如果您要保存到软盘，请插入软盘并点击 OK。数据将保存到软盘中。

此操作的结果是在软盘目录中创建了 `knopix.sh` 和 `configs.tbz` 文件。`configs.tbz` 文件包含了来自 `/home` 和 `/etc` 目录的所有保存配置。`knopix.sh` 文件是一个脚本，告诉 KNOPPIX 在启动时如何安装这些文件。下次您启动 KNOPPIX 时，可以使用下一节介绍的方法使用这些配置文件。

> 那些创建了自己 KNOPPIX 启动盘的用户可以将他们的 `knopix.sh` 和 `config.tbz` 文件添加到 CD 的根目录下，这样 KNOPPIX 就会直接启动他们的个性化配置，而无需担心额外的软盘或介质。

# 重启 KNOPPIX

您通过插入 KNOPPIX CD 或 DVD 并重启电脑来启动 KNOPPIX。然而，如果您想利用设置的持久磁盘或保存的配置信息，您需要在 KNOPPIX 启动提示符中添加一些选项。方法如下：

- 1. 将 KNOPPIX CD 或 DVD 插入计算机（这适用于书中附带的 DVD）并重启。您将看到 KNOPPIX 启动提示符。
- 2. 在 KNOPPIX 启动之前按 F3，查看是否需要额外的启动选项。
- 3. 如果您有配置软盘启动盘（或在之前的操作中创建的其他可移动介质），请插入该磁盘。
- 4. 在启动提示符处，输入以下命令行之一，这些是加载配置文件的不同方式：

```
boot: knoppix floppyconfig
```
```
boot: knoppix myconfig=/dev/hda
```
```
boot: knoppix myconfig=/dev/sda
```
```
boot: knoppix myconfig=scan
```

这些 KNOPPIX 启动命令分别从软盘获取配置信息、在第一个 IDE 驱动器分区 (`/dev/hda1`) 查找信息、在第一个 SCSI 分区 (`/dev/sda`) 查找信息，或扫描所有驱动器寻找信息。要启动持久桌面（假设您之前设置过），可以输入：

```
boot: knoppix home=/dev/hda1/knoppix.img
```
```
boot: knoppix home=/dev/sda/knoppix.img
```
```
boot: knoppix home=scan
```

之前的启动命令分别将 KNOPPIX 目录 (`/home/knoppix`) 分配给 `/dev/hda/knoppix.img` 文件、`/dev/sda/knoppix.img` 文件，或通过扫描所有可用目录找到的镜像。您可以从上述每组命令中组合一个来读取您的配置文件并分配持久桌面，例如：

```
boot: knoppix floppyconfig home=/dev/hda1/knoppix.img
```

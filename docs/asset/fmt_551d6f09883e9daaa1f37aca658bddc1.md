
3. 记住在做出更改后保存文件。

4. 确保所有 PC 卡均已正确插入，并重启 Linux。
5. 在重启期间，倾听一系列蜂鸣声，这指示你的 PC 卡是否被 `cardmgr` 守护进程识别并配置。代码请参见表 9.1。

另请参考
了解如何重启 Linux，请参阅第 13 页。
关于编辑文本文件的更多信息，请参阅第 64 页。

| 蜂鸣声数量/类型 | 指示 |
|---|---|
| 一声蜂鸣 | PC 卡已弹出 |
| 两声高音 | PC 卡在启动期间被识别并配置 |
| 高音、低音 | PC 卡已 识别，但在启动期间未被配置 |
| 低音蜂鸣 | PC 卡未被识别 |
| 两声高音 | PC 卡已插入 |
| 两声高音 | 重启或关机期间卸载了 PC 卡服务 |

某些卡（如闪存卡、驱动器和 CD-ROM 适配器）必须由文件系统挂载。为了实现这一点，你需要编辑 `/etc/fstab` 或将该卡作为新新驱动器手动挂载到系统中。

另请参考
学习如何使用 `/etc/fstab` 数据库或文件系统表，请参阅第 124 页。
关于挂载驱动器系统的更多信息，请参阅第 124 页。

140

## 使用 cardmgr 命令

`cardmgr` 守护进程用于监控电脑的 PC 卡插槽是否有插入或移除的卡，并将加载或卸载 PC 卡所需的设备。适当的驱动程序位于 `/etc/pcmcia` 目录下的 `config` 文件的 `cardmgr` PC 卡数据库中。你的卡的数据库条目告诉 `cardmgr` 守护进程加载或卸载哪个代码模块。（代码模块通常位于 `/lib/modules/kernel-version` 目录下。）

### 列出你的 PC 卡和驱动程序

启动时，或当 PC 卡插入或弹出时，`cardmgr` 守护进程会在 `/var/run` 目录下创建并更新一个系统表。要查看当前使用的 PC 卡和驱动程序列表，请如下查看此系统表：

```
# cat /var/run/stab

socket 0: empty

socket 1: Serial or Modem Card

1      serial_cs      0       ttyS1   4       65
```

此特定的 `stab` 文件显示有两个可用的 PC 卡插槽（`socket 0` 和 `socket 1`），其中包含一个串口或调制解调器，该卡使用 `serial_cs` 代码模块为 `/dev/tty1` 设备提供串口服务。如果插入了另一块卡，`cardmgr` 守护进程将执行以下操作：

1. 它记录插入操作。
2. 在 `/etc/pcmcia/config` 数据库中查找。
3. 它尝试加载适当的模块。
4. 如果卡被识别并配置，它会响两声蜂鸣。

随后 `/var/run/stab` 文件将更新这些新信息，看起来可能如下：

```
# cat /var/run/stab

socket 0: fixed      0       hdc    22      0

socket 1: Serial or Modem Card

1      serial_cs      0       ttyS1   4       65
```

这显示 `socket 0` 中的固定磁盘被检测、识别并配置为硬盘，使用 `/dev/hdc` 卷，而使用 `/dev/tty1` 串口端口的串口或调制解调器卡仍留在 `socket 1` 中。

## 第二部分 配置你的系统

## 第 9 章 启用 PC 卡设备

### 禁用 cardmgr 命令事件通知

在你确定 PC 卡已被正确识别后，可以通过编辑 `pcmia` 启动脚本或配置文件来静任何 `cardmgr` 蜂鸣通知。在 `pcmia` 脚本中使用 `cardmgr` 命令时，使用 `-q`（静音）命令行选项。更改后，当在启动 Linux 时使用 `cardmgr` 命令识别并配置你的 PC 卡时，你将听不到任何蜂鸣声。（我保持开启它，这样如果没听见声音，我就知道出问题了。）

### 禁用 PC 卡通知

1. 确保你以 root 操作员身份登录。
2. 使用你喜欢的文本编辑器打开文件 `/etc/init.d/pcmia`。此文件的路径根据你的发行版而异，因此请检查你发行版的文档以了解系统初始化脚本的位置。
3. 寻找脚本中包含 `cardmgr` 命令的部分。它看起来像这样：
   `/sbin/cardmgr $SCARDMR_OPTS`
4. 在 `cardmgr` 命令中添加 `-q`（静音）选项：
   `/sbin/cardmgr -q $SCARDMR_OPTS`
5. 保存更改并退出。
6. 重启 Linux。

另请参考
关于你的发行版存放启动脚本的位置，请参阅你发行版的文档。
关于编辑文本文件的更多信息，请参阅第 64 页。

### 使用 cardctl 命令

使用 `cardctl`（卡控制）命令来控制你的 PC 卡。这是笔记本电脑用户在物理移除卡的情况下节省电池电的好方法。

#### 获取 PC 卡状态

要检查任何卡的状态，请使用 `cardctl status`，如下：

```
# cardctl status

socket 0: empty

socket 1: Serial or Modem Card

1      serial_cs      0       ttyS1   4       65
```

#### 列出你的 PC 卡配置

要查看你的 PC 卡配置，请使用 `cardctl config` 选项，如下：

```
# cardctl config

socket 0: fixed      0       hdc    22      0

socket 1: Serial or Modem Card

1      serial_cs      0       ttyS1   4       65
```

### 挂起和恢复 PC 卡电源

对于带有 PC 卡的笔记本用户，节省电池的另一种方法是挂起和恢复卡的电源。`cardctl` 命令允许你通过 `suspend` 命令关闭并禁用插槽，如下：

```
# cardctl suspend 0
```

这将关闭并断开插槽 0。在执行 `suspend` 命令后恢复该插槽以使用，请使用 `resume` 命令行选项，如下所示：

```
# cardctl resume 0
```

# 第 10 章

## 添加指针设备

### 添加鼠标

安装摇杆

### 添加鼠标

Linux 对鼠标的支持非常广泛。它支持多种设备。虽然在运行 X 窗口系统（X Window System）时可以使用键盘来控制鼠标指针，但使用鼠标或其他硬件设备来控制指针是必不可少的。你将使用鼠标拉下菜单、点击对话框中的按钮，以及在程序之间复制和粘贴文本。

当你安装 Linux 时，系统可能会引导你通过一个简短的程序来配置鼠标。安装程序实际上会检查你是否插入了任何指针设备，并尝试为你检测它们的类型。如果没有找到任何设备，将为你提供鼠标设备列表供选择。通常情况下，“3 键鼠标”选项即可。随后会创建一个符号链接 `/dev/mouse`，它指向正确的指针设备。要查看 `/dev/mouse` 指向系统中的哪个设备，可以使用如下 `ls`（或列出目录）命令：

```
# ls -1 /dev/mouse

lrwxrwxr-x 1 root root 5 Mar 07:54 /dev/mouse -> psaux
```

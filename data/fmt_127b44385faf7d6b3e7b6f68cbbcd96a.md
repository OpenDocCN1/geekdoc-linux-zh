
了解如何寻找文件将在 RHCE 考试期间为你节省大量时间。按照以下步骤熟悉熟悉 Linux 源码树：

1. 如果你之前没有安装 Linux 内核源码，请安装 `kernel-source`、`kernel-headers` 和 `kernel-doc` 软件包。

2. 检查 `/usr/src/linux` 目录及其子目录。找到表 17.2 列出的每个文件和目录。

### 安装内核 tar 文件

```bash
cd /usr/src
mkdir linux-version
rm linux
ln -s linux-version linux
zzvf linux-version.tar.gz
```

其中 `version` 是 tar 文件包含的 Linux 内核版本。一旦文件安装，你就可以按照下一章提供的程序构建内核。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_423_0.png)

某些内核存档使用 BZIP 工具压缩内核，这会产生更小的存档文件。有关使用 BZIP 工具的说明，请参阅其帮助页。

### 内核模块

内核模块是包含动态加载内核组件的文件，例如设备驱动程序。Linux 2.0 需要外部协助来加载和卸载模块；然而，Linux 2.2 引入了 `kmod` 线程，可以在需要时自动加载模块。

本节描述了内核模块所在地、内核模块配置文件 `/etc/conf.modules` 以及管理内核模块的主要命令：

- `depmod`，创建一个描述模块依赖关系的数据库
- `lsmod`，列出已加载的模块
- `modprobe`，加载内核模块
- `rmmod`，卸载内核模块

#### 模块位置

内核模块的标准位置是目录 `/lib/modules/version`，其中 `version` 是相关 Linux 内核的版本号。Red Hat 的 `extraversion` 代码确保了同一发布版本的不同内核的模块不会发生冲突。

要查看运行内核的版本和 `extraversion` 代码，请执行

```bash
uname -r
```

该命令的输出仅包含内核版本和 `extra-version` 代码。例如：

```
2.4.5-15
```

与示例内核相关的模块位于 `/lib/modules/2.4.5–15`。

内核模块目录包含几个子目录。通常包括：

- `block`，包含与块设备相关的模块
- `cdrom`，包含与 CD-ROM 设备相关的模块
- `fs`，包含与文件系统相关的模块
- `ipv4`，包含与 TCP/IP 模块
- `misc`，包含模块类型
- `net`，包含与网络相关的模块
- `pcmcia`，包含与 PCIA 模块
- `scsi`，包含与 SCSI 模块
- `video`，包含与视频相关的模块

#### 列出模块

要查看加载了哪些模块，请执行 `lsmod` 命令。以下是典型输出：

```
lsmod
Module Size Used By
```

命令的输出报告：

- 每个模块的名称
- 每个模块的大小
- 模块的使用次数
- 引用该模块的其他模块名称

现在你已经学会了 `lsmod`，完成练习 17.5。

### 练习 17.5

#### 查看模块

`lsmod` 命令非常简单，对管理非常有帮助。为了更好地熟悉该命令，请使用它识别系统中的模块。

#### 卸载空闲模块：`rmmod`

当模块空闲 10 分钟时，`/etc/cron.d/kmod` 将卸载它。然而，你可以随时通过执行命令卸载模块

```bash
rmmod module
```

其中 `module` 是你想卸载的空闲模块。你可以指定多个模块，用一个或多个空格分隔每个模块名。指定多个模块的顺序无关；命令同时删除它们。如果模块在使用或被加载的模块引用，则无法删除。要删除所有模块，执行命令

```bash
rmmod -a
```

### 练习 17.6

#### 卸载驱动

通常不需要卸载模块，但对于 RHCE 考试，了解如何操作很重要。如果你的系统包含配置好的声卡，你可以执行以下步骤来了解更多模块：

1. 确保没有应用程序在使用声适配器。
2. 使用 `lsmod` 识别模块。查看模块名称并判断哪些可能是声模块。
3. 使用 `rmod` 卸载声模块。由于由于某些模块被其他模块使用，你可能会发现无法按任意顺序卸载模块。如果某个模块无法卸载，尝试另一个。继续尝试直到删除所有声模块。

#### 加载模块：`modprobe` 和 `insmod`

要加载模块，执行格式如下的命令

```bash
modprobe module.o
```

或者更简单：

```bash
modprobe module.o
```

其中 `module.o` 是包含编译模块的对象文件名。如果模块接受或需要参数，请在命令行包含它们——例如：

```bash
modprobe fancycard.o irq=11 align=no
```

412 第 17 章 · 理解内核

如果指定的模块需要其他模块，`modprobe` 将通过搜索由 `depmod` 命令构建的数据库来自动查找并加载它们，该命令将在随后的子节中描述。

`modprobe` 命令有两种主要的运行模式。在一种模式下，它可以使用单个模块名称或一系列候选名称进行探测。当你指定一个系列且 `modprobe` 成功加载了某个候选模块时，它将停止探测。要启动探测，使用如下形式的命令：

```
modprobe -t dir pattern
```

其中 `dir` 指定 `/lib/modules/version` 的一个子目录，`pattern` 是指定候选模块文件名的正则表达式。例如，要从 `/lib/modules/2.4.5-15` 目录加载模块（假设当前运行的内核版本为 2.4.5-15），执行命令：

```
modprobe -t net '*'
```

在另一种主要模式下，`modprobe` 命令尝试加载特定目录中的每一个候选模块。例如，尝试加载 `/lib/modules/2.4.5-15/misc` 目录中的所有模块，执行命令：

```
modprobe -a -t misc '*'
```

当然，你不太可能尝试加载每一个模块。相反，应该使用一个仅识别相关模块文件的模式。与 `modprobe` 命令类似，`insmod` 命令也可以加载内核模块。然而，`insmod` 命令不会尝试加载依赖模块。因此，`modprobe` 命令更为常用，但在那些以自己的方式处理模块依赖而非使用 `modprobe` 的脚本除外——因为这些脚本可能在系统启动期间执行，而那时模块依赖数据库可能尚未更新。如果你的 Linux 系统有音频适配器，请完成练习 17.7，以获得加载驱动程序的实践经验。

### 练习 17.7

#### 加载驱动程序

为了配置 Linux 系统使用新的硬件设备，你通常必须加载一个作为该设备驱动程序的模块。有时有必要加载一个提供特殊功能的模块，例如 FTP 传输的 IP 伪装。如果你的系统有音频适配器，可以进行此练习，让你练习模块的操作。

Copyright©2000 SYBEX, Inc., Alameda, CA www.sysex.com

#### 练习 17.7（续）

- 1. 确保没有应用程序正在使用音频适配器。
- 2. 如果必要，使用 `rmmod` 卸载音频驱动程序。
- 3. 使用 `modprobe` 为显卡加载正确的驱动程序。

你可以回顾前面的章节和练习 17.6 的结果来获得帮助。在参加 RHCE 考试之前，请确保你已经如何在没有书籍或笔记辅助的情况下加载模块。

### 更新模块依赖数据库：`depmod`

`modprobe` 正确识别依赖于其他模块的模块并将它们作为一个组加载的能力是非常方便的。然而，正常运行取决于一个更新的模块列表，该列表标识了每个模块所需的其他模块。`depmod` 命令构建包含这些信息的数据库 `/etc/rc.d/rc.sysinit` 脚本在每次系统启动时都会调用 `depmod` 命令来建立这样的数据库。

```
depmod -a
完全重新构建模块数据库。
```

### 配置模块：`/etc/conf.modules` 文件

`/etc/conf.modules` 文件允许你指定多种控制 `depmod` 和 `modprobe` 操作的参数。例如，你可以：

字体 使用别名（Aliases）通过更方便的名称引用模块

- 在模块加载时传递给模块的默认参数（Parameters）
- 在模块加载或卸载时执行的 Shell 命令

以下是一个典型的 `/etc/conf.modules` 文件：

```
alias sound emu10k1
alias parport_lowlevel parport_pc
alias eth0 3c90
alias eth1 3c90
options opl3 io=0x388
preinstall emu10k1 insmod soundcore
post-remove emu10k1 rmmod soundcore
```

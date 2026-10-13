
最显著的区别是，你不再需要用模块前缀（如 `Cwd::`）来限定子程序名。

你可以使用 `require` 或 `use` 来包含模块。在使用这些函数时请记住以下细微差别：

- 当通过调用 `require` 包含模块时，只有在 `require` 函数被执行时模块才会被包含。
- 当通过 `use` 包含模块时，模块在 `use` 语句被处理时就会被包含。

## 808 理解 Perl 对象

你如何知道应该调用哪些方法以及按什么顺序调用它们呢？
在使用对象之前，你必须阅读该对象的文档。
方法名和方法调用的序列取决于该对象的功能。

## 使用 English 模块

Perl 包含了几个名称奇特的特殊变量，例如 `$_`（用于默认参数）和 `$`（用于对应上一个错误的消息）。在阅读程序时，可能很难猜测某个特殊变量的含义。结果就是，你可能会避开一个对你的程序可能很有用的特殊变量。

作为一种友好的辅助，Perl 5 提供了 English 模块（`English.pm`），它允许你使用易于理解的名称来表示 Perl 中的特殊变量。要使用 English 模块，请在你的 Perl 程序中包含以下行：

```
use English;
```

之后，你可以将 `$_` 称为 `$ARG`，将 `$` 称为 `$ERRNO`（这些英语英语名称可能有点晦涩，但绝对比标点符号要好得多）。

以下程序使用了 English 模块，并打印了几个有趣的变量：

```
#!/usr/bin/perl -w

# File: english.pl

use English;

print "Perl executable = $EXECUTABLE_NAME\n";

print "Script name = $PROGRAM_NAME\n";
```

使用以下命令运行此脚本：

```bash
./english.pl
```

当我在 Red Hat Linux 上运行此脚本时，输出如下：

```
Perl executable = /usr/bin/perl

Script name = ./english.pl
```

English 模块非常实用，因为它让你在编写 Perl 脚本时可以使用有意义的名称来引用特殊变量。要了解更多关于 Perl 特殊变量及其英语名称的信息，请在终端窗口输入 `man perlvar` —— 或者更好，将浏览器指向：

`http://www.perdoc.com/perl15.8.0/pod/perlvar.html`

## 附录：关于 DVD

### 本附录内容

- 系统要求
- DVD 安装说明
- 你将在 DVD 上找到的内容内容
- 故障排除

## 系统要求

确保你的计算机符合列表所示的最低系统要求。如果你的计算机不符合这些大部分要求，你在使用 DVD 上的软件和文件时可能会遇到问题。

- 配有 133 MHz Pentium 级处理器的 PC（图形模式建议使用 400 MHz Pentium II 或更高型号）
- 计算机至少安装 64MB 总内存用于文本模式，图形模式需要 128MB；为了获得最佳性能，我们建议图形模式至少 256MB
- 一个 DVD-ROM 驱动器（如果你只有 CD-ROM 驱动器，请使用附带的券自行 CD-ROM 版本的 Red Hat Linux）
- 能显示至少 256 色色的显卡和显示器
- 声卡
- 以太网卡接口 (`NIC`) 或速度至少 65 Kbps 的调制解调器
- 硬盘至少有 650MB 空闲空间用于最小安装；工作站级安装建议 2.6GB

## DVD 安装说明

从 DVD 安装 Red Hat Linux 可能会有些复杂，因为 PC 某些硬件不受 Red Hat Linux 支持。尽管如此，配套 DVD 上的 Red Hat Linux 已经支持广泛的硬件，因此你的 PC 外围设备很都都支持。

## 810 DVD 安装说明

要从配套 DVD 安装 Red Hat Linux，请遵循以下步骤。（如需最新、最全的信息，请参考 DVD-ROM 根目录下的 `README` 文件。）

- 1. 在安装 Linux 之前，收集你的 PC 硬件信息，例如显卡、网卡和 SCSI 卡。
- 2. 使用分区程序（如 `PartitionMagic` 或 `FIPS` 程序）为 Red Hat Linux 在硬盘上创建空间。

如果你计划将 Red Hat Linux 作为 PC 上唯一的操作系统，或者计划将其安装在空的第二个硬盘上，请跳过此步。

- 3. 如果你的 PC 无法从 DVD 驱动器启动，请创建一个 Red Hat Linux 启动盘。
- 4. 使用 DVD 或 Red Hat Linux 启动盘启动 PC。

此步骤会自动运行 Red Hat Linux 安装程序。从现在开始，在多个窗口中回答问题，Red Hat Linux 安装程序将引导你完成各个步骤。以下是一些关键步骤：

- 识别 PC 上安装的任何 SCSI 适配器。
- 为 Red Hat Linux 准备硬盘分区。如果你通过缩小现有 DOS 分区创建了空间，此步骤将允许你为 Red Hat Linux 创建分区。
- 配置以太网（如果有的话）。你可能需要指定参数，例如 Red Hat Linux 系统的 IP 地址和主机名。
- 指定本地时区并设置 `root` 密码。
- 在硬盘上安装引导加载程序，以便在关机后开启 PC 时可以启动 Red Hat Linux。
- 选择你想安装的软件包，例如 X Window 系统以及 GNOME 或 KDE 图形桌面。
- 配置 X Window 系统并启用图形登录，这样当你启动 Linux 系统时，它会显示登录框，并在成功登录后直接进入 GNOME 或 KDE 图形桌面。

要从 DVD 安装特定软件包，请遵循以下步骤：

- 1. 以 `root` 身份登录。
- 2. 将 DVD 插入计算机的驱动器。
- 3. 如果你使用 GNOME 或 KDE GUI，请等待 DVD 挂载。否则，打开终端窗口并在命令提示符输入 `mount`

```bash
mount /mnt/cdrom
```

- 4. 选择主菜单；系统设置；添加/删除应用程序。

`Add and Remove Software` 工具将启动并收集有关系统中已安装软件包状态的信息。在处理完所有已安装软件包的信息后，该工具将显示所有软件包的列表。窗口左侧有两个大按钮——Install Software（安装软件）和 Remove Software（删除软件）。默认选中 Install 按钮。

- 5. 要安装任何未安装的软件包，点击该软件包对应的 Install 超链接。

会出现一个对话框，详细说明你将安装的内容以及新软件包所需的磁盘空间。

- 6. 点击 Install Packages（安装软件包）来安装选软件包。
- 7. 要从 DVD 驱动器移除 DVD，输入以下命令：

```bash
umount /mnt/cdrom
```

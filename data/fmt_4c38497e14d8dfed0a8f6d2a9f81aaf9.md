
# 内核计时器与编译选项

你向我问了更多问题，其中一些你可能应该坚持关注的。首先，内核计时器具有多年来一些争论的益处，而 TCK 的默认 500Hz 在通用内核的意义上很糟糕，而低延迟内核使用的是 1024Hz。最后，如果你能够运行非实时（或任何其他内核配置）内核，这是一个喝茶的好时，因为内核源码可以被克隆、打补丁并配置。任何内核补丁都可以手动构建，但脚本可以帮助。在任何内核作为 DEB 包构建之前，应该始终关注 `/boot` 目录的遗迹。我们喜欢涵盖更多内核补丁，特别是 Xarmor，但你之后需要学习这些。如果你想选择任何内核，可以：

```bash
sudo apt install git
sudo git clone https://github.com/Foraging/linux-linux.git
cd linux-linux
```

那里有一个安装脚本可以供你找到。还有一个 `cfg` 自定义文件，如果你想影响脚本的行为。如果你选择某些通用选项，但如果应该工作（DEB 包可以像其他包一样安装）。接下来，你会被询问想要安装哪个内核版本。最新的，从前沿（RCs）到稳定的 5.4 版本，似乎比你运行的更快。然后你将获得 CPU 调度器（选择 CBQ）的选择以及编译器选择。

![](img/97fdf078658cf34e6c480f18f1f2014d_38_1.png)

`clang` 3 具有... (+14 特性)

- 开始
- 调试
- 报告 Bug
- 行星系

当你浏览完说明文档并知道每项涉及什么后，点击标记为 'Run' 的按钮来启动救援。

| | Rescue MENU | | | |
|---|---|---|---|---|
| Rescue GRUB Menu | Easy Boot Fix | Restore Menu | Update GRUB Menu |
| Easy Boot Fix | | | |
| check boot grub on partition | | | |
| Filesystem Fix (fsck) | | | |
| Password | | | |
| Change GRUB Password | separate passwords | Blank password | |
| Windows | | | |
| Restore Windows Media (USB) | | | |
| Reinstall Windows to unlock this Windows | | | |
| GPT | | | |
| Delete | create new partition table | check boot grub on partition | |

# Rescue 恢复工具

如果运行 Linux 或 Windows，这是一个恢复电脑的一站式生命线。许多事情可能会搞乱电脑。不小心按键可能会删除文件、重写引导程序、搞登录屏幕或导致可怕的问题。如果你发现陷入绝境，停止并获取 Rescue (http://rescue.org/)。Live 提供了丰富的工具集合，你可以用它解决各种常见问题。如果你需要修复 Windows 分区或安装问题，Rescue 也会非常有用。该发行版整合了所有修复无法启动的 Linux 和 Windows 问题的重要实用工具，包括 testdisk、photo 和 GParted。你可以使用 Rescue 恢复引导程序、修复文件系统错误、修复分区表并重置 Linux 和 Windows 密码。它还包含了恢复数据和还原文件的工具，并可以在无数据的情况下擦除两者。

![](img/97fdf078658cf34e6c480f18f1f2014d_39_0.png)

有几个面向救援的发行版，但 Rescue 因其直截了当而运行。与其他只提供一组工具来修复损坏电脑的发行版不同，Rescue 具有许多功能用于引导你处理特定问题的过程。该发行版旨在作为 Live 介质使用，因此插入或连接启动介质（USB 驱动）到受影响的电脑并启动。从 Rescue 中你可以得到基于 LXDE 的极简图形桌面。当调用 Rescue 时，它会自动启动你的系统。

> Rescue 的目的是帮助你从灾难中恢复，它还封装了 GPG 等工具，帮助保护你的系统并防止无意的隐私泄露。

界面在最新版本中有所改进。菜单分为不同的类别，如 Grub、文件系统和启动。每个类别内部的按钮都有清晰的标签，帮助你识别它们。当你点击其中一个时，它会打开一个窗口解释 Rescue 将采取哪些步骤以及对你的要求。在你浏览完插图文档并知道每项包含的内容后，点击标记为 'Run' 的按钮来启动救援。

# 编译器与内核优化

某些发行版，如 Alpine 和 Android，功能非常少（以及工具各自的）。大多数发行版仍使用 GCC 编译它们的内核，但多年来使用 Android 和 ChromeOS 等是可能的。OpenLLVM（底层虚拟机）是一个基于 C++ 语言编写的工具，以及 GNU 扩展。使用 Clang 而不是 GCC 有技术原因，特别是对于不同平台的组合。使用 Clang 编译的二进制文件（LLVM 中间表示）可以针对任何 LLVM 后端，构建内核仅支持 ARM 和 x86，但对于其他的（MIPS、RISC-V、PowerPC）可用。此外，可以使用静态和动态分析工具调查内核。这些工具可以帮助我们发现 bug。这意味着使用 Clang 编译内核将提高性能。事实上，自从 Linux 5.2（2021年2月）以来，内核已支持 LTO（链接时优化）。这项练习使内核作为一个整体进行优化，而不是在单个文件的上下文中。

# Grub 引导修复

Grub 引导程序的许多问题可以通过点击“Boot-App 修复”一键按钮来解决。这款实用的应用程序具有直观的用户界面，可以扫描并检测各种 Linux 分区，并正确识别其中的操作系统。该工具既适用于使用 MBR 布局的 Windows 电脑，也适用于使用 GPT 布局的 UEFI 电脑。在 Rescacity 工具的“专家工具（Expert Tools）”类别下可以使用 Boot-Repair。当启动它时，程序将扫描您的硬盘，并向您显示由几个标签页组成的简单界面。您可以遵循建议，只需点击“建议修复（Recommended repair）”，这应该能解决大多数问题。在恢复您的电脑后，工具还会获取一个短 URL，您应当记录。该 URL 包含了您的磁盘、分区的详细摘要，以及重要 Rescu 文件的内容，包括 `/etc/grub` 和 `boot/grub.cfg`。如果问题仍然存在，可以将该 URL 分享到您的发行版论坛版块，以便他人了解您的磁盘情况并提供建议。

最好从 Live CD 进行修复以防损坏分区。要做到这一点，请启动 Rescacity 并选择“文件系统检查（修复）[File System Check (Fixed)]”选项列出所有分区。这将显示某个分区存在错误，Rescacity 将扫描并修复任何不一致之处。

Linux 最常见的问题之一是引导程序无法工作。它无法帮助您启动一台不稳定的电脑。主引导记录（MBR）位于硬盘的特殊区域，有助于跟踪所有分区的位置，并存储引导代码。

Rescacity 包含多个选项，用于重新生成引导程序并修复 MBR。其中包含“恢复 Grub（Restore Grub）”选项，它将重写引导代码并从 `/etc/grub` 文件中恢复您的标识符。

Linux 不会连接到所有分区，但它将允许您选择想要安装 `grub-grub` 的分区。如果您有多个磁盘，菜单将提示您选择磁盘并根据启动顺序对它们重新排序。

完成后，如果您使用的是基于 Debian 的发行版，该工具将安装新的引导程序并将其放置在 MBR 中。如果您想添加其他基于 Debian 的系统，它将引导您完成系统设置。

该工具的新版本还允许您删除 Linux GRUB 引导项。您可以根据意愿，在运行 `update-grub` 之前进行 Rescacity 检查，并最终留在 grub 界面。

在组中，您将仅被要求选择主磁盘且其包含数据。此新选项将向您显示上述两个任务的信息。

如果您遇到过系统崩溃，可以在不丢失数据的情况下进行恢复。与其通过终止进程来修复微小故障，不如安装 Rescacity 并毫不费力地完成它。该发行版为 Linux 和 Windows 系统提供了恢复选项。

如果您拥有 Windows 分区的密码，请安装 Rescacity 并选择“Windows 密码（Windows Password）”选项。该发行版将扫描您的电脑以寻找包含安全账户管理（SAM）的分区。[等待，根据上下文，流程见下文]

安全账户管理（SAM）。如果您只使用一个分区还好，但如果您有多个 Windows 系统，该工具将显示多个分区。请选择包含您想要恢复的用户密码的分区。

> 使用“工具/磁盘检测并去重（Tool/Disk Detect de-duplicate）”选项，选择扫描和修复以找到丢失的分区并恢复它们。

> Rescacity 基于 Debian，并包含您可以用于安装恢复工具的系统。

Rescacity 将在删除分区之前恢复注册表文件。然后您选择想要擦除的分区。擦除后，您可以重启电脑，进入 Windows 并使用该工具为您选择的用户重置 Windows 密码。

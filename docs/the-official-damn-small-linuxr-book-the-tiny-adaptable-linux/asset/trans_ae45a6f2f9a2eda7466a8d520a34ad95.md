

+   3. 使用 pendrive.bat 启动 DSL。
+   4. 在 Qemu 中运行的 DSL 中，在你的主目录中添加文件并更改设置。
+   5. 从 DSL 下载你需要的任何扩展到 /cdrom/mydsl 目录。
+   6. 从 DSL，点击 DSLpanel，点击 Backup/Restore，然后点击 Backup。
+   7. 从 DSL 菜单中，选择 Apps->Net->SMBclient 并输入你的具体信息以连接（Domain、Machine、Share、Name 和 Password）。然后，从 SMB 提示符输入以下内容：
+   
+   smb:\> lcd /cdrom
+   smb:\> put backup.tar.gz
+   smb:\> lcd mydsl
+   smb:\> cd mydsl
+   smb:\> put just_downloaded_extension
+   
+   （对所有新下载的扩展重复此操作）
+   
+   smb:\> quit
+   8. 关闭 DSL。

## 使用你的 DSL-Embedded 配备的 U 盘进行原生 BIOS 启动

本主题在第 6 章“运行原生 U 盘安装”中有所介绍，但我想提到的是，在 BIOS 识别 U 盘为可启动之前，你必须先将 Syslinux 应用到驱动器上。有一个可在 Windows 中使用的 Syslinux 版本，但我们收到的反馈是，有时它与用户的系统并不完全兼容。你始终可以通过从本书提供的 LiveCD 启动 Damn Small Linux 来设置 Syslinux。

请务必阅读 dsl-embedded.zip 文件中的 readme.txt。里面有一些提示，如果你遇到困难可能会有用。

## 使用 KQemu 提高 Qemu 的性能

那么，你认为拥有一个嵌入式 Linux 系统很酷，但希望速度能快一点？Qemu 开发者为你提供了解决方案。

KQemu 是一个 Qemu 加速器，效果很好。在我的实验中，我将虚拟启动时间减少了一半。这是一个伟大的发展，使得运行 DSL-Embedded 更加愉快。

在 DSL-Embedded bat 文件（1st-boot.bat、dsl-base.bat、dsl-vhd.bat 和 printer.bat）的默认配置中，我们让 Qemu 在未启用 KQemu 的情况下运行。你必须修改你选择的配置的 .bat 文件以启用 KQemu 加速。

查找 qemu.exe 命令行上的以下选项：

```
-no-kqemu
```

将其替换为

```
-kernel-kqemu
```

你需要在以下位置下载 KQEMU 的 Microsoft Windows 版本：

http://www.h7.dion.ne.jp/~qemu-win/

在撰写本文时，版本 Kqemu-1.3.0pre11-install.exe 可用。下载并安装 KQEMU 后，你需要运行以下命令：

```
net start kqemu
```

要么将其输入到运行命令中，要么打开命令提示符并在其中输入该命令。图 7-2 显示了从运行实用程序启用 KQemu 的示例：

![](img/af53325d7f38f1cdafca9f44568e4ab8_166_0.png)

**FIGURE 7-2** Enter `net start kqemu` into the Run utility.

这应该就是你需要做的所有事情来享受加速性能。现在以通常的方式启动 DSL-Embedded。

## 在 VMPLAYER 中运行 DSL——VMWARE 的免费虚拟机

VMPlayer 是 VMWare 的免费虚拟机。它是免费下载的，但不可自由分发。VMPlayer 背后的部分技术是开源的，显然是在 GPL 下许可的。我们将探讨在 Microsoft Windows 环境中使用 VMPlayer 虚拟机运行 Damn Small Linux。

图 7-3 显示了在 Windows XP 中在 VMPlayer 中运行 Damn Small Linux 的示例。

![](img/af53325d7f38f1cdafca9f44568e4ab8_167_0.png)

# FIGURE 7-3 Damn Small Linux running in VMPlayer on a Windows XP host system.

## 比较 VMPlayer 与 Qemu

在许多方面，Qemu 和 VMPlayer 的性能基准测试是相当的。一些研究表明，带有 KQEMU 加速器的 Qemu 在性能上领先。在我有限的测试中，VMPlayer 启动更快，并且在一般使用过程中似乎在资源上挣扎得更少。可能是我们的 Qemu 默认设置限制了系统；我们将不得不做进一步的测试来弄清这种差异。

VMPlayer 比 Qemu 大得多（25MB 对比不到 2MB），并且需要在主机操作系统上安装。因此，没有办法像 QEMU 那样从低影响的 U 盘运行 VMPlayer。如果你处于使用 Windows 计算机的情况，并且想要一种回到运行


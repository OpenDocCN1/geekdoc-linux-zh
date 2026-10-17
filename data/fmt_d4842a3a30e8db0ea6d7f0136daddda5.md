
| tcl_trg | 8.0.5-1 | BSD | tcl 是一种简单的脚本语言，设计用于嵌入其他应用程序中。tcl 设计用于与 tk 使用（tk 是一个小部件集，由 tk 包提供）。该包还包含了 tcl，一个 tcl 程序的简单示例。如果您正在安装 tcl 包并想要进行开发，应该也安装 tk 和 tcl 包。 |

| util-linux_trg | 2.9w-1 | distributable | util-linux 包包含了 Linux 系统运行所必需的各种低级实用程序。在许多功能中，util-linux 包含了 fdisk 配置工具和登录程序。 |

## BlueCat Linux 的优缺点

我们现在转向问题列表，来询问任何嵌入式 Linux 工具包，以查看 BlueCat Linux 与竞争对手相比如何。

## 生成的镜像有多大？

与本章稍后检查的 PeeWeeLinux 一样，BlueCat 受到使用 glib 作为其 C 库的影响。这使得在存储空间小于 2MB 的嵌入式设备中很难放入功能。然而，BlueCat 在软磁盘上可以放置更多内容。

## 支持哪些架构？

支持以下处理器族：

- Intel IA32 (x86)
- PowerPC
- ARM7/ARM9
- MIPS R3000/R4000

### 使用该工具包需要什么要求？

支持以下主机系统：

- Red Hat 6.1 和 6.2
- TurboLinux 工作站，6.0 版本
- Windows 98/NT/2000

Windows 通过 cygwin 支持。

## 工具包易用吗？

该工具包非常直观。

### 可以在不丢失更改的情况下安装新版本的工具包吗？

即使我们的示例位于 `/bluecat/bluecat` 目录树中，但没有理由必须这样做。您可以轻松升级 BlueCat 而不会毁掉您的项目。

2. 将发行包解压到至少有 150MB 空闲空间的文件系统中（仅二进制文件）。

3. 解压后，你将获得一个名为 `Embedded_Build` 的新目录。进入该目录并运行 `.pwqlconfig` 脚本。该脚本是 PeeWeelinux 的核心——这是一个 20KB 的 bash 脚本，用于构建和配置你的项目并构建可启动的镜像。

4. 管理包文件（Manage Package Files），然后提取所有 RPM 文件。在执行此操作之前，你将没有任何可选择的包。

5. PeeWeelinux 自带了几个示例项目。我建议你不要从头构建新项目；因为很难判断一个项目需要哪些包，不如直接从其中一个示例包开始。例如，要从最小化包开始，只需从 PeeWeelinux 根目录解压，将 `projects/minimal` 重命名为 `projects/yourprojectname` 并重新运行 `.pwqlconfig`。你应该选择包含所有管理项目（Manage Projects）中的项目。

最小项目包含以下所有内容：

- 编辑器：ee
- 内核：basic 2.2.17，带有极简模块
- Shell：ash
- 系统基础：bflush, dev, filesystem, initscripts, mingetty, sysvinit, util-linux
- 系统库：glibc, libtermcap
- 系统工具：fileutils, sh-utils, textutils

6. 选择“配置文件系统”（Configure File System）来选择哪些包放入你的文件系统中。最小化包几乎占满了整个软盘，因此无法放入 Minicom。然而，PeeWeelinux 也带了 microcom，它只有 12KB，所以选择该包（网络串口 Network Serial 下）作为示例。

7. 选择“为项目提取文件系统”（Extract File System for Project）。这会将包的所有内容复制到项目项目下的 `mnt` 目录中——为下一步做好准备。

8. 将软盘插入驱动器并选择“将文件系统加载到目标”（Load File System onto Target）。如果一切顺利，你将获得一个可启动的软盘。

9. 启动软盘。你需要登录——root 密码为 redhat。登录后，输入 `microcom /dev/ttySx` 来运行 microcom。根据你测试的串口端口，将 x 更改为 0 或 1。

## PeeWeLinux 包含哪些？

PeeWeLinux 实际上包含了许多包，每个包都经过重新编译，以完美适配嵌入式 Linux 环境。

| 包 | 版本 | 许可证 | 描述 |
| --- | --- | --- | --- |
| ICACClient | 3.0-1 | 商业授权 | Citrix 指示计算架构 (ICA)。 |
| XFree86 | 3.3.6-7 | MIT | X窗口系统为开发图形用户界面提供了基础技术。此包包含 X 工作站所需的基础文件。然而，此包未为显卡提供特定的硬件 X 服务器。 |
| XFree86-Xdpifonts | 3.3.6-7 | MIT | 当 X 为 75 或 100 时。这些包包含了大多数 Windows 系统使用的字体。 |
| XFree86-X | 3.3.6-7 | MIT | 当 X 为 3DLabs, 8514, AGX, FBDev, I128, Mach32, Mach64, Mono, P9000, S3, S39, SVGA, VGA16, W32 或 Xnest 之一时。这些包为许多视频芯片组提供了特定的硬件 X 服务器。 |
| XFree86-libs | 3.3.6-7 | MIT | XFree86 大部分 X 程序所需的共享库 |
| XFree86-stuff | 3.3.6-7 | MIT | 使用 XFree86 构建的各种程序和工具 |
| XFree86-twm | 3.3.6-7 | MIT | 适用于 Windows 系统的简单窗口管理器 |
| XFree86-xdm | 3.3.6-7 | MIT | 管理可能位于本地主机或远程服务器上的 X 显示集 |
| XFree86-xfs | 3.3.6-7 | MIT | 包含 XFree86 xfs 的字体服务器，xfs 也可以向远程服务器提供字体 |
| ash | 0.2-2 | BSD | 大多数 Linux 发行版使用 GNU/bash (Bourne again shell)。然而，bash 是一个非常大的程序，需要大量内存。 |

## PeeWeLinux 包含哪些？

| 包 | 版本 | 许可证 | 描述 |
| --- | --- | --- | --- |
| ICACClient | 3.0-1 | 商业授权 | Citrix 指示计算架构 (ICA)。 |
| XFree86 | 3.3.6-7 | MIT | X窗口系统为开发图形用户界面提供了基础技术。此包包含 X 工作站所需的基础文件。然而，此包未为显卡提供特定的硬件 X 服务器。 |
| XFree86-Xdpifonts | 3.3.6-7 | MIT | 当 X 为 75 或 100 时。这些包包含了大多数 Windows 系统使用的字体。 |
| XFree86-X | 3.3.6-7 | MIT | 当 X 为 3DLabs, 8514, AGX, FBDev, I128, Mach32, Mach64, Mono, P9000, S3, S39, SVGA, VGA16, W32 或 Xnest 之一时。这些包为许多视频芯片组提供了特定的硬件 X 服务器。 |
| XFree86-libs | 3.3.6-7 | MIT | XFree86 大部分 X 程序所需的共享库 |
| XFree86-stuff | 3.3.6-7 | MIT | 使用 XFree86 构建的各种程序和工具 |
| XFree86-twm | 3.3.6-7 | MIT | 适用于 Windows 系统的简单窗口管理器 |
| XFree86-xdm | 3.3.6-7 | MIT | 管理可能位于本地主机或远程服务器上的 X 显示集 |
| XFree86-xfs | 3.3.6-7 | MIT | 包含 XFree86 xfs 的字体服务器，xfs 也可以向远程服务器提供字体 |
| ash | 0.2-2 | BSD | 大多数 Linux 发行版使用 GNU/bash (Bourne again shell)。然而，bash 是一个非常大的程序，需要大量内存。 |

*(注：此处为原文重复的表格翻译)*

| 包 | 版本 | 许可证 | 描述 |
| --- | --- | --- | --- |
| ICACClient | 3.0-1 | 商业授权 | Citrix 指示计算架构 (ICA)。 |
| XFree86 | 3.3.6-7 | MIT | X窗口系统为开发图形用户界面提供了基础技术。此包包含 X 工作站所需的基础文件。然而，此包未为显卡提供特定的硬件 X 服务器。 |

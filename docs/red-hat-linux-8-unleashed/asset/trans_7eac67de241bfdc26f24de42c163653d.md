
Win4Lin 使用原生的 Windows 程序和 dll，但在安装 Windows CD 期间对其中某些部分进行了修改。安装完 CD 后，每个用户必须使用合法的 MS Windows 许可安装自己的 Windows 副本；出于安全考虑，禁止 root 用户（超级用户）运行 Win4Lin 桌面。你真的希望 Windows 对你的电脑拥有 root 权限吗？Windows 的安装将正常进行，只是比你习惯的速度要快。

## 配置 Win4Lin

作为 root 用户，你可以在 Win4Lin 中进行系统级设置，并通过 GUI 界面启用硬件。你可以从 root 桌面上通过 xterm 命令行运行 `winsetup` 来访问该界面，如下：

```
$ winsetup
```

Win4Lin 有一些命令行选项，但它们使用起来很麻烦——为了为 root 安装一个最小化的桌面环境（如果还没有的话）以便使用 GUI 工具更省事。root 用户仅负责 Win4Lin 的系统级管理；他她无法使用 Win4Lin 以 root 身份运行 Windows。

### 作为个人用户

> 提示
> 你必须在 winsetup 程序中启用剪切和粘贴，即使如此，它在 Win4Lin 中也可能无法正常工作。Red Hat 提供了 xcutsel 工具来交换剪切和粘贴剪贴板缓冲区。从命令行启动 xcutsel（你可能想创建一个桌面快捷方式以便方便使用）并尝试交换剪贴板。xcutsel 工具可能适用于其他应用程序。

## 启动 Win4Lin 会话

从命令行启动 Win4Lin 会话以启动 Windows 会话或 DOS 会话：

```
$ win
```

或者

```
$ dos
```

Win4Lin 也可以提供 MS DOS 环境，因为 Windows 已经包含了它。这个 DOS 可能比在 Bochs 下运行的 FreeDOS 提供的更有用且更易配置。虽然存在命令行选项，但除了最冷门的选项外，所有选项都通过 winsetup 应用程序处理。这些冷门选项是遗留产，当时 Win4Lin 的前身程序 Merge 运行 16 位的 Windows 二进制文件，并需要访问 8086 Intel 处理器的高级内存管理功能。

启动后，Win4Lin 会在一个运行你 Linux 桌面的 X 窗口中提供 MS Windows 桌面。你可以像处理 X 会话一样将 Win4Lin 导出到另一台计算机。Win4Lin 的单用户版本一次仅支持一个用户；该产品提供服务器版本。名为 apprapper.exe 的不支持的应用程序（在 Netverse 网站上可用）可用于显示运行 Win4Lin 中的单个应用程序，而不是整个桌面——如果你出于安全考虑想限制用户对应用程序的选择，这非常有用。

## 比较 Wine、Win4Lin 和 VMware

那么 Win4Lin 和 VMware 模拟器与 Wine 程序之间如何比较？Wine 相比 VMware 的优势在于它的成本更低且占用的资源更少。另一方面，Win4Lin 无法处理 VMware 能处理的各种操作系统，而且硬件支持更加有限。

Win4Lin 也具有一些 Wine 不具备的优点。Win4Lin 可以运行更广泛的应用程序，并且比 Wine 更稳定；它比相同硬件上的原生 Windows 安装运行速度更快、更稳定。然而，Win4Lin 的成本确实比 Wine 高，而且你必须拥有获得授权的 Windows 副本才能使用它。

Win4Lin 非常适合运行各种业务相关的应用程序，如 MS Office（面向办公，而非面向家庭或多媒体的 DirectX/3D），并在一个对稳定性至关重要且有授权 Windows 副本的环境中使用。

## Mac OS 模拟

Apple 提供了一个吸引了数百万忠实追随者的操作系统，并且存在大量的应用程序。对于模拟器开发者来说，在 Intel 硬件上模拟 Apple Macintosh 操作系统是一项挑战。Apple 软件设计为运行在非 Intel 处理器以及与许多基于 Intel 的 PC 不同的硬件上。一个重大的障碍是必须拥有合法的 Apple ROM 代码。Red Hat 不提供任何 Apple 模拟器。

在本节中，我们将查看可用的最流行且成熟的 Apple 模拟器，看看它们能为 Apple 用户提供什么。如果你已经有一台 Apple 设备并积累了相关软件，这些模拟器可以通过让你在单台计算机上使用所有应用程序，为它们注入新的活力和易用性。

## EXECUTOR

ARDI 的 Executor 是一款商业软件模拟器，可以在 Linux 下运行旧版 Mac OS 应用程序。在购买之前，可以从 http://www.ardi.com 下载演示版本进行测试。Executor 模拟运行 System 6.0.7 的 Motorola MC68040 CPU，并支持近 400 个 Macintosh 应用程序。然而，某些不支持的功能和硬件包括串口端口、LocalTalk、控制面板或 INITs。另一方面，Executor 不需要 Apple Mac OS 系统文件或二进制 ROM 镜像。

> 注意
> Executor 不运行较新的 OS X 应用程序。然而，你可以通过 http://gnu-darwin.sourceforge.net/ 下载并安装 Apple 的 Darwin 发行版。但是它不包含专有的 OS X 图形界面，因此无法运行那些应用程序。你最好安装 Darwin 所基于的完整版 BSD：http://www.freebsd.org。

该软件通过 rm 命令在 /executor/bin 目录下进行安装，并指向 /usr/local/bin 目录的符号链接。客户端启动方式如下：

```
$ executor
```

按下回车键后，主窗口将如图 27.9 所示。

![图 27.9](http://example.com/image_27_9.png)
图 27.9 使用 Executor 运行程序。软件遵循 X11 窗口设置。左 Alt 键用作 Apple Command 键，而右 Alt 键用作 Option 键。按下 Alt+5 设置偏好。

## Basilisk II

Basilisk II 是一款免费的 Macintosh 模拟器，为了运行特定的 Mac 软件提供了 PowerPC 模拟。运行 Basilisk II 需要早期版本的 OS 副本和 Apple ROM 芯片。它支持多个版本的 OS，最高到 8.1。Red Hat Linux 不支持分级文件系统 (HFS+)，但支持早期的 HFS。

Basilisk II 还支持以太网、串口、SCSI 和 Apple 桌面总线 (ADB) 驱动。你可以使用图形编辑器设置；可以在家目录下编辑名为 .basisk_prefs 的文件。你可以用它指定各种硬盘、软磁盘、视频分辨率、色彩深度、声音、键盘、鼠标、网络和服务器端口，以及文件位置、分配内存和启动模式。

你可以从头下载并构建 Basilisk II 模拟器。你可以在 Basilisk II 主页（后文引用）找到源码压缩包或 RPM 包。关于 Basilisk II 问题和安装的优秀网络参考是 http://www.karning.net/-mhoffman/basiskII/system7/linux/。

## 远程操作系统

现代操作系统支持远程管理和访问工具；Linux 也例外。许多传统的 UNIX 命令（如 rep 和 telnet）已被更强大、更安全的客户端取代。本节提供了 VNC 的概述和介绍。VNC 是你 Red Hat CD-ROM 中包含的一种流行的网络客户端。它允许在你的计算机上显示一个远程计算机桌面的窗口。你的本地鼠标和键盘控制远程计算机，就像你坐在它面前一样。在本节中，我们将研究 VNC 并展示如何安装和运行它，以及一些实用的 VNC 变体。

## Virtual Network Computing

Virtual Network Computing（简称 VNC）是由英国 AT&T 实验室制造的一种虚拟网络管理应用程序。VNC 包含 vserver 和 vncviewer 组件；你使用 VNC 访问网络计算机上的远程桌面。主机必须运行原生的 vnc，但你可以在任何地方运行它。数十种操作系统都提供免费下载的 VNC 版本。

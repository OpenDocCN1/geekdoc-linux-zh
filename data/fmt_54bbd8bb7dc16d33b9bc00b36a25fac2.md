
"Windows printer via Samba" 指的是位于 Windows 网络上的打印机。你需要指定 Windows 服务器（主机名或 IP 地址）、共享的名称、打印机的工作组名称以及用户名和密码。共享是 `smb` URL 格式 `\hostname\printername` 中的主机名和打印机名称。服务器是放置打印机的计算机。用户名和密码可以是打印机资源本身的，也可以是特定用户访问的。面板将在顶部显示一个框，你可以在其中输入共享主机和打印机名称作为 `smb` URL。你可以使用下方的框从网络上 Windows 主机的列表中选择打印机，而不是输入 URL。例如，如果你的 Windows 网络是 WORKGROUP，那么将显示条目 WORKGROUP，你可以展开它以列出该网络上的所有 Windows 主机（如果你的网络是 MSHOME，则将列出该名称）。当你做出选择时，相应的 URL 将显示在 `smb://` 框中。在面板底部，输入任何需要的 Samba 认证信息，如用户名或密码。然后你可以使用 `lpr` 等打印客户端将文件打印到 Windows 打印机；`lpr` 将调用 Samba 客户端 `smbclient` 将打印任务发送到 Windows 打印机。

要访问 SMB 共享远程打印机，你需要安装 Samba 并启用使用 `smb` 守护进程的 Server Message Block 服务。为此，请确保在 `system-config-services`（System | Administration | Servers Settings | Services 菜单）中启动带有 `smb` 条目的 Samba，并勾选其复选框以便每次启动时自动运行。反过来，必须在 Windows 网络上启用打印机共享。

## X Window System 配置：system-config-display 和厂商驱动程序

你桌面显示的 GUI 接口由 X Window System 实现。Fedora 上使用的版本是 X.org (`x.org`)。X.org 为各种显卡和显示器提供自己的驱动程序。你可以使用 `system-config-display` 工具配置显示设置，以更改屏幕分辨率设置，以及选择显示器或视频卡驱动程序。

作为替代方案，你可以下载并安装由 ATI 或 Nvidia 等显卡供应商提供的驱动程序和视频配置工具。这些由第三方软件库提供，特别是 Livna。由于许可问题，它们不属于 Fedora 软件库。安装后，你可以使用它们自己的配置工具来配置显示（Applications | System Tools 菜单）。与 X.org 驱动程序相比，厂商驱动程序通常提供更多选项，例如 3d 加速，尽管 X.org 驱动程序往往更稳定。

### system-config-display

如果你想更改显示设置，或者在 X Window System 配置方面遇到困难，你可以使用 `system-config-display` 来更改配置。你可以通过选择 System | Administration 菜单上的 Display 来运行 `system-config-display`。`system-config-display` 工具打开一个带有三个面板的 Display Settings 窗口：Settings（设置）、Hardware（硬件）和 Dual Head（双头显示）（如图 4-7 所示）。

Settings 面板显示用于选择分辨率和颜色深度的弹出菜单。当前的分辨率和颜色深度已经选中。

要更改显示器或视频卡设置，点击 Hardware 选项卡。这将显示一个包含 Monitor 和 Video Card 条目的面板。每个都有一个 Configure 按钮。点击 Video Card 的 Configure 按钮会显示支持的显卡列表。最初仅显示 Generic CRT 和 LCD 条目。点击 Show All Available Monitors 复选框以显示包含可扩展厂商条目的完整列表。Reset default 按钮将返回到你的默认条目。视频卡配置通常不应使用，但对于在相同卡的不同驱动程序之间切换可能很有用，例如 X.org nv NVIDIA 驱动程序和 NVIDIA 提供的 nvidia 驱动程序。

对于支持双头连接的显卡，你可以使用 Dual Head 面板来配置第二个显示器。首先你启用双头显示，然后可以配置连接到第二个端口的显示器。对于 Desktop Layout，你可以拥有独立的桌面或跨越两个显示器的扩展桌面。

`system-config-display` 工具随后生成一个名为 `/etc/X11/xorg.conf` 的 X Window System 配置文件。这是 X Window System 启动时使用的文件。Fedora 使用 X.org 驱动程序用于 X Window System。你可以在 www.x.org 上了解更多关于 X.org 的信息。每当更改设置时，当前配置都会保存到 `/etc/X11/xorg.backup.conf`。如果需要手动恢复旧设置，只需将当前的 `xorg.conf` 替换为备份文件即可。

## 视频显卡驱动程序支持：ATI、NVIDIA 和 Livna

虽然 Fedora 包含通用的 Xorg NVIDIA 和 ATI 驱动程序，但为了充分利用你的显卡驱动程序，你必须使用厂商提供的 NVIDIA 或 ATI 驱动程序。NVIDIA 和 ATI 都提供兼容 Linux 的驱动程序版本，几乎每月发布一次。驱动程序包含更新的错误修复和增强功能。

你可以直接从厂商网站或通过 Yum 使用 Livna 准备的版本下载并安装这些驱动程序。始终建议使用 Livna 版本的厂商图形驱动程序。Livna 版本已经过测试和配置，专门用于在 Fedora 上使用，而直接的厂商软件包是通用的，旨在用于所有 Linux 系统。很可能在直接尝试使用厂商图形软件包时会遇到困难，而 Livna 版本通常没有问题。Livna 仍然是专门内核驱动程序和模块的最佳软件库，即使其其他多媒体软件包可能会与其他软件库发生冲突。即使你禁用 Livna，你仍然希望使用它来用于图形和 NTFS 驱动程序，以及其他专用驱动程序。

Livna 提供的图形驱动程序使用两个软件包，一个用于支持软件，另一个用于内核。在 `rpm.livna.org` 网站上，你会找到针对每个内核版本列出的 ATI 和 NVIDIA 模块。`Yum` 将自动检测你的内核版本并选择正确的模块软件包。此外，针对不同类型的内核（如 Xen 或 PAE）也有内核模块。同样，`Yum` 将检测要使用的正确模块软件包。如果你想手动安装模块软件包，你必须知道你的内核版本和类型以选择正确的软件包。要找出你的内核版本，可以使用命令 `uname -r`。

NVIDIA 将其驱动程序组织为三个驱动程序软件包：用于当前卡片的软件包，用于 9600 系列卡片的 96xx 软件包，以及用于过时卡片的 legacy 软件包。此外，

Livna 提供了支持软件的开发包，以及其 SRPMS 目录中驱动程序源码包。以下是针对当前显卡的 NVIDIA 驱动程序包：

```
xorg-x11-drv-nvidia-driver-version.i386.rpm
kmod-nvidia-kernel-version_FC7.i586.rpm
```

ATI 软件包使用的术语是 `fglrx`，而非 ATI。ATI 仅使用单一的驱动集合，包含一个支持软件包和一个内核模块包。Livna 为每个内核版本和内核类型提供模块包，`Yum` 会自动检测这些包。与 NVIDIA 类似，ATI 也提供用于支持软件的开发包。Livna 网站还在其 SRPMS 目录中提供驱动程序的源码包。

```
xorg-x11-drv-fglrx-driver-version.i386.rpm
kmod-fglrx-kernel-version_FC7.i586.rpm
```

最好始终使用 `Yum` 来安装驱动程序。`Yum` 会自动检测正确的内核版本。你只需对内核模块使用初始的唯一名称，例如 ATI 的 `kmod-fglrx`。ATI 驱动软件也会作为依赖项被选中，在此情况下为 `xorg-x11-drv-fglrx`。`Yum` 会检测剩余的软件包名称，并选择适合你内核的软件包。对于 NVIDIA，你在 `yum` 命令中使用 `kmod-nvidia`，这将同时检测并选择 `xorg-x11-drv-nvidia`，即 NVIDIA 驱动软件。

若要使用 `Yum` 安装图形驱动程序，请确保已安装 Livna Yum 仓库支持。从 `rpm.livna.org` 网站下载并安装适用于你的 Fedora 发行版的 `livna-release` 软件包。安装完成后，你就可以通过 `Yum` 访问所有 Livna 软件。你可以使用 Pirut（应用程序 | 添加/删除软件）或在终端窗口中使用 `yum` 命令。如果使用 Pirut，请选择“搜索”面板，并输入 NVIDIA 的字符串 `kmod-nvidia` 或 ATI 的 `kmod-fglrx`。然后选择你想要安装的内核模块软件包。
